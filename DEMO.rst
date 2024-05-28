PRESENTACIÓN ORAL
-----------------

Buenos días. Hoy os vamos a presentar las funcionalidades y mejoras implementadas durante este último sprint. En esencia, el equipo se ha centrado en la implementación de la seguridad y en la gestión de usuarios, compras, facturación y transacciones.

Comenzaré por mostrar todo lo relacionado con la seguridad. Hemos implementado autenticación mediante credenciales y autorización mediante roles. Se han establecido tres grupos principales de usuarios: administrador, trabajador y cliente, cada uno con sus permisos asignados. [MOSTRAR LOS PREPARADOS EN LA BD]. Además, se ha añadido la encriptación de contraseñas para garantizar la privacidad y seguridad.

Ahora, vayamos al Swagger. Como podéis ver, Swagger muestra todas las opciones y métodos disponibles, aunque estos son inaccesibles hasta que se complete el proceso de autenticación del usuario. Una vez autenticado, se harán accesibles los métodos dedicados a cada rol de usuario.

Hemos implementado un registro mediante el cual podemos añadir nuevos usuarios. [DEMOSTRACIÓN]. Una vez registrado, el usuario podrá acceder al método de login, donde, añadiendo sus credenciales (email y contraseña), recibirá un token. Con este token, el usuario se dirigirá a la parte superior del Swagger, donde se encuentra el botón de Authenticate. Aquí añadirá el token recibido por el login, autenticándose en el servicio. [DEMOSTRACIÓN CON CADA ROL UN MÉTODO AL QUE PUEDE ACCEDER Y UNO AL QUE NO]. 

Finalmente, el usuario, al terminar sus gestiones, podrá hacer logout mediante nuestro método personalizado. Además, el token tiene un tiempo de caducidad para forzar el cierre de sesión automáticamente. Como podéis ver, para hacer logout no es necesario aportar ninguna credencial, ya que este método solo funciona si el usuario se ha autenticado previamente.

[¿DEBEMOS DE MENCIONAR ESTO?]
Cabe mencionar que estamos trabajando en brindar al usuario la posibilidad de cambiar su contraseña una vez establecida, pero no os lo podemos mostrar en esta demo.
   






USER:
    • Añadir método modificar datos de tu usuario.
       
SHOPPINGCART:
    • Añadir posibilidad de tener 3 carritos.
    • Poder realizar varias compras.
    • Controlar los cambios de stock en las compras.
      
INVOICE:
    • Corrección datos de la factura.
    • Posibilidad de descargar la factura.
    • Añadir diferentes idiomas para los correos y las facturas.
    • Mostrar todas las facturas de un usuario.

TRANSACTIONS:
    • Añadir calculo ingresos, gastos y beneficios por fechas.

PRODUCT SUPPLIER TRANSACTIONS
    • Incorporar facturas de un proveedor (comprar y devolver)
    • (PRODUCTS) ver historial de compras de un producto concreto a un proveedor.
    • (SUPPLIER) ver historial de compras a un proveedor.

TODO EN GENERAL:
    • Controlar todas las respuestas de todos los métodos.



PREPARACIÓN TÉCNICA
-------------------

SECURITY
========

La clase ``SwaggerConfig`` es parte de la configuración de tu aplicación y se encarga de establecer cómo se maneja la seguridad en la documentación interactiva de tu API. Vamos a desglosar lo que hace y sus principales características. 

La clase configura Swagger para que reconozca y utilice un esquema de seguridad basado en ``tokens JWT`` (JSON Web Tokens). Esto significa que para acceder a las funciones de la API, los usuarios deben proporcionar un token válido, que autentica sus peticiones.

``createAPIKeyScheme`` define el tipo de esquema de seguridad que la API utilizará. En este caso, se especifica que se usará un esquema de tipo ``bearer`` con formato JWT.

``openAPI`` añade los requisitos de seguridad y los esquemas definidos anteriormente para que Swagger los utilice.

La clase usa la anotación ``@Configuration``, lo que indica que es una clase de configuración en Spring.


.. code-block:: java

   @Configuration
   public class SwaggerConfig {
   
       private SecurityScheme createAPIKeyScheme() {
           return new SecurityScheme()
                   .type(SecurityScheme.Type.HTTP)
                   .bearerFormat("JWT")
                   .scheme("bearer");
       }
   
       @Bean
       public OpenAPI openAPI() {
           return new OpenAPI()
                   .addSecurityItem(new SecurityRequirement().addList("Bearer Authentication"))
                   .components(
                           new Components()
                                   .addSecuritySchemes("Bearer Authentication", createAPIKeyScheme()));
       }
   }

..


La clase ``SecurityConfig`` es parte de la configuración de seguridad de tu aplicación. Esta clase se asegura de que solo los usuarios autenticados puedan acceder a ciertas partes de la aplicación y define cómo deben manejarse las peticiones y sesiones.

Configura cómo se deben proteger las rutas y recursos de tu aplicación.

Establece los filtros de autenticación y define las políticas de manejo de sesiones.

``PasswordEncoder`` se utiliza para encriptar las contraseñas de los usuarios.

``UserDetailsService`` carga los detalles del usuario (como nombre de usuario y contraseña) desde una fuente de datos.

``JwtService`` maneja la generación y validación de tokens JWT, que se utilizan para autenticar a los usuarios.

``securityFilterChain`` configura la cadena de filtros de seguridad:

   * ``csrf disabled``  porque se utiliza una política de sesión sin estado. El servidor no almacena información sobre las sesiones de los usuarios. La información necesaria para autenticar y autorizar al usuario se envía con cada petición.

   * ``authorizeHttpRequests`` permite el acceso a ciertas rutas sin autenticación. Todas las demás peticiones requieren autenticación.

   * ``frameOptions.disable()`` permite que el contenido se cargue en iframes, necesario para la consola H2.

   * ``JWTAuthenticationFilter`` añade un filtro de autenticación JWT antes del filtro de autenticación estándar.

   * ``sessionManagement - SessionCreationPolicy.STATELESS`` configura las sesiones como sin estado (no se mantienen entre peticiones).

   * ``cache.requestCache`` utiliza una política de caché que no almacena las peticiones.

``authenticationProvider`` define el proveedor de autenticación:

``DaoAuthenticationProvider`` es un servicio de detalles de usuario y encriptador de contraseñas.
   
``authenticationManager`` configura el gestor de autenticación, que maneja el proceso de autenticación.


.. code-block:: java

   @Configuration
   public class SecurityConfig {
   
       private final PasswordEncoder passwordEncoder;
       private final UserDetailsService userDetailsService;
       private final JwtService jwtService;
   
       public SecurityConfig(
               PasswordEncoder passwordEncoder,
               JwtService jwtService,
               UserApiServiceImpl userDetailsService) {
           this.passwordEncoder = passwordEncoder;
           this.userDetailsService = userDetailsService;
           this.jwtService = jwtService;
       }
   
       @Bean
       public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
           http.csrf(AbstractHttpConfigurer::disable)
                   .authorizeHttpRequests(
                           auth -> {
                               auth.requestMatchers(new AntPathRequestMatcher("/h2-console/**"))
                                       .permitAll();
                               auth.requestMatchers(
                                               "/v3/api-docs/**",
                                               "/swagger-ui/**",
                                               "/login/**",
                                               "/register/**")
                                       .permitAll();
                               auth.anyRequest().authenticated();
                           })
                   .headers(headers -> headers.frameOptions(frameOptions -> frameOptions.disable()))
                   .addFilterBefore(
                           new JWTAuthenticationFilter(userDetailsService, jwtService),
                           UsernamePasswordAuthenticationFilter.class)
                   .sessionManagement(
                           session -> session.sessionCreationPolicy(SessionCreationPolicy.STATELESS))
                   .requestCache(cache -> cache.requestCache(new NullRequestCache()));
   
           return http.build();
       }
   
       @Bean
       public AuthenticationProvider authenticationProvider() {
           DaoAuthenticationProvider authenticationProvider = new DaoAuthenticationProvider();
           authenticationProvider.setUserDetailsService(userDetailsService);
           authenticationProvider.setPasswordEncoder(passwordEncoder);
           return authenticationProvider;
       }
   
       @Bean
       public AuthenticationManager authenticationManager(AuthenticationConfiguration config)
               throws Exception {
           return config.getAuthenticationManager();
       }
   }

..


La clase ``JWTAuthenticationFilter`` es un filtro que se ejecuta una vez por cada solicitud HTTP en tu aplicación. Este filtro se encarga de la autenticación de los usuarios mediante tokens JWT.

Verifica si las peticiones HTTP contienen un token JWT válido.

Extrae la información del usuario del token y autentica al usuario en el contexto de seguridad de Spring.

``UserDetailsService``: Este servicio carga los detalles del usuario (nombre de usuario, contraseñas, roles, etc.) desde una fuente de datos.

``JwtService``: Este servicio maneja la creación, extracción y validación de los tokens JWT.

``doFilterInternal``:

   * ``extractUsername(token)``: Obtiene el encabezado de autorización (Authorization) de la petición HTTP. Divide el encabezado para obtener el token si está presente y comienza con la palabra "Bearer".

   * ``jwtService.validateToken(token, userDetails)``: Si el token está presente y es válido, extrae el nombre de usuario del token usando jwtService. Carga los detalles del usuario (roles, permisos, etc.) desde userDetailsService.

   * ``setAuthentication(authToken)``: Si el token es válido y los detalles del usuario son correctos, se crea un objeto de autenticación (UsernamePasswordAuthenticationToken) y se establece en el contexto de seguridad de Spring (SecurityContextHolder).

   * ``filterChain.doFilter(request, response)`` Finalmente, la petición continúa a través de la cadena de filtros (filterChain), permitiendo que otros filtros de seguridad y lógica de negocio se ejecuten.


.. code-block:: java

   public class JWTAuthenticationFilter extends OncePerRequestFilter {
   
       private final UserDetailsService userDetailsService;
       private final JwtService jwtService;
   
       public JWTAuthenticationFilter(UserDetailsService userDetailsService, JwtService jwtService) {
           this.userDetailsService = userDetailsService;
           this.jwtService = jwtService;
       }
   
       @Override
       protected void doFilterInternal(
               HttpServletRequest request, HttpServletResponse response, FilterChain filterChain)
               throws ServletException, IOException {
           String authorizationHeader = request.getHeader("Authorization");
           String[] authHeaderArr =
                   authorizationHeader != null ? authorizationHeader.split(" ") : null;
           String token = null;
           String username = null;
   
           if (authHeaderArr != null && authHeaderArr[0].equals("Bearer")) {
               token = authHeaderArr[1];
               username = jwtService.extractUsername(token);
           }
   
           if (username != null && SecurityContextHolder.getContext().getAuthentication() == null) {
               UserDetails userDetails = userDetailsService.loadUserByUsername(username);
               if (Boolean.TRUE.equals(jwtService.validateToken(token, userDetails))) {
                   UsernamePasswordAuthenticationToken authToken =
                           new UsernamePasswordAuthenticationToken(
                                   userDetails, null, userDetails.getAuthorities());
                   authToken.setDetails(new WebAuthenticationDetailsSource().buildDetails(request));
                   SecurityContextHolder.getContext().setAuthentication(authToken);
               }
           }
   
           filterChain.doFilter(request, response);
       }

..


La clase ``LoginController`` se encarga de gestionar el proceso de autenticación de usuarios en tu aplicación. Proporciona un punto de acceso (endpoint) que permite a los usuarios autenticarse y recibir un token JWT (JSON Web Token) para futuras peticiones. 

Autentica a los usuarios que intentan iniciar sesión con su email y contraseña.

Si la autenticación es exitosa, genera y devuelve un token JWT.

``tokenList``: Almacena temporalmente los tokens JWT emitidos para los usuarios.

``@Tag``: Proporciona metadata para la documentación de Swagger.

``@RestController`` y ``@RequestMapping``: Indican que esta clase es un controlador de Spring que maneja peticiones HTTP en la ruta /login.

``(@PostMapping) loginUser``:

   * Recibe el email y la contraseña del usuario como parámetros.
   
   * Autentica al usuario mediante authenticationManager.
   
   * Carga los detalles del usuario con userDetailsService.
   
   * Si la autenticación es exitosa, verifica si ya existe un token JWT válido para el usuario.
   
   * Si no existe un token válido, genera uno nuevo y lo almacena en tokenList.
   
   * Devuelve una respuesta con el token JWT y los detalles del usuario (nombre de usuario, roles).

``isTokenExpired``:

   * Verifica si un token JWT ha expirado.

   * Intenta parsear el token para comprobar su validez; si el token ha expirado o es inválido, devuelve true.

``createJwt``:

   * Crea un nuevo token JWT con una validez de 10 horas.
   
   * Establece el nombre de usuario como sujeto y firma el token con la clave de firma proporcionada por jwtService.


.. code-block:: java

   @Tag(name = "login", description = "Endpoint to authenticate as an existing user")
   @RestController
   @RequestMapping("/login")
   public class LoginController {
   
       private final UserDetailsService userDetailsService;
       private final JwtService jwtService;
       private final AuthenticationManager authenticationManager;
       private final Map<String, String> tokenList = new ConcurrentHashMap<>();
   
       public LoginController(
               AuthenticationManager authenticationManager,
               UserApiServiceImpl userApiService,
               JwtService jwtService) {
           this.authenticationManager = authenticationManager;
           this.userDetailsService = userApiService;
           this.jwtService = jwtService;
       }
   
       @PostMapping
       public ResponseEntity<LoginResponseDTO> loginUser(String email, String password) {
           Authentication authentication =
                   authenticationManager.authenticate(
                           new UsernamePasswordAuthenticationToken(email, password));
           UserDetails user = userDetailsService.loadUserByUsername(email);
   
           if (authentication.isAuthenticated()) {
               String token = tokenList.get(email);
               if (token == null || isTokenExpired(token)) {
                   token = createJwt(email);
                   tokenList.put(email, token);
               }
               return ResponseEntity.ok(
                       LoginResponseDTO.builder()
                               .jwt(token)
                               .username(user.getUsername())
                               .roles(user.getAuthorities())
                               .build());
           }
   
           return new ResponseEntity<>(HttpStatus.NOT_FOUND);
       }
   
       private boolean isTokenExpired(String token) {
           try {
               Jwts.parser().verifyWith(jwtService.getSigningKey()).build().parseSignedClaims(token);
               return false;
           } catch (ExpiredJwtException | IllegalArgumentException e) {
               return true;
           }
       }
   
       public String createJwt(String username) {
           return Jwts.builder()
                   .subject(username)
                   .issuedAt(new Date())
                   .expiration(new Date(System.currentTimeMillis() + 1000 * 60 * 60 * 10)) // 10 hours
                   .signWith(jwtService.getSigningKey())
                   .compact();
       }


















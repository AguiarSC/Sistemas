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

   * Extracción del Token: Obtiene el encabezado de autorización (Authorization) de la petición HTTP. Divide el encabezado para obtener el token si está presente y comienza con la palabra "Bearer".
   * Validación del Token: Si el token está presente y es válido, extrae el nombre de usuario del token usando jwtService. Carga los detalles del usuario (roles, permisos, etc.) desde userDetailsService.
   * Autenticación del Usuario: Si el token es válido y los detalles del usuario son correctos, se crea un objeto de autenticación (UsernamePasswordAuthenticationToken) y se establece en el contexto de seguridad de Spring (SecurityContextHolder).
   * Continúa la Cadena de Filtros: Finalmente, la petición continúa a través de la cadena de filtros (filterChain), permitiendo que otros filtros de seguridad y lógica de negocio se ejecuten.



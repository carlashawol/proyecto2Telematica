# Documento Final(Análisis y Documentación)

Análisis y Diseño:

1.	Definición de Equipo (integrantes, emails)
2.	Asignación de roles y responsabilidades de cada integrante del equipo en el desarrollo del proyecto2.
3.	Especificación de requisitos no funcionales.
a.	Disponibilidad
El sistema debe soportar 2.000 sesiones concurrentes.
b.	Rendimiento
El sistema debe tener una latencia menor a 1 segundo para todas las peticiones.
El sistema debe disponer de autoescalabilidad en la base de datos.
c.	Seguridad
El sistema debe permitir realizar autenticación SSO con un proveedor externo.
El sistema debe permitir realizar una autenticación de dos factores, realizada con un proveedor externo.
El sistema debe contar con firewall en servidores.
El sistema debe tener seguridad en la aplicación, mediante análisis de código estático y bloqueo de acceso.
El sistema debe contar con técnicas de seguridad para contraseñas.
El sistema debe contar con detección de ataques de intrusos, verificación de integridad de mensajes.

4.	Diseño para la Escalabilidad (disponibilidad, rendimiento y seguridad)
a.	Qué patrones de arquitectura específicos (patrones de escalabilidad y buenas prácticas) se utilizarán en el SISTEMA para apoyar esta escalabilidad:
i.	Mejores prácticas
Arquitectura simple, Diseñar componentes de software modulares, estrategia de almacenamiento en caché, cifrar bajo el dominio URL de servicios externos, utilización de owast.
ii.	Selección de tácticas 
Prevenir fallas, reparar fallas, detectar fallas, Detección de intrusos, Detección de denegación, Verificar la integridad de los mensajes.
iii.	Decisiones de diseño 
   Asignación de responsabilidades, modelo de coordinación, Modelo de datos, Gestión de recursos, mapeo entre elementos arquitectónicos, Selección de tecnología, redundancia, virtualización y replicación.

b.	Definición de Herramientas para utilizar:
Maquinas EC2
Balanceadores de carga
Ip elástica
RDS
VPC
Diseño e implementación de CDN
CloudFare
Servicios Externos (Facebook y Google)
Plugins en wordpress (Se especifica más adelante)

Proceso de instalación y DevOps:
Documentación del DNS
El Sistema de Nombres de Dominio o DNS es un sistema de nomenclatura jerárquico que se ocupa de la administración del espacio de nombres de dominio (Domain Name Space). Su labor primordial consiste en resolver las peticiones de asignación de nombres. Esta función se podría explicar mediante una comparación con un servicio telefónico de información que dispone de datos de contacto actuales y los facilita cuando alguien los solicita. Para ello, el sistema de nombres de dominio recurre a una red global de servidores DNS, que subdividen el espacio de nombres en zonas administradas de forma independiente las unas de las otras. Esto permite la gestión descentralizada de la información de los dominios
Para asignar el dominio utilizamos name.com

Pasos seguidos para asignar el dominio:
Paso 1: Se busca el dominio en name.com para ver si está disponible y se selecciona uno.
 
Paso 2: Se siguen los pasos para comprar el dominio, que incluye crear una cuenta en name.com
 


Paso 3: luego se accede a la administración del dominio desde la cuenta asociada.
 

Paso 4: Se accede al servidor de nombres del dominio
 

Paso 5: Se colocan los nombres de servidor proporcionados por cloudflare
 

PASOS SEGUIDOS PARA CAMBIAR EL NOMBRE DEL DNS:
Paso 1: Obtener el dominio.
Paso 2: Ir a cloudflare y registrarse.
Paso 3: Hacer click en add site y colocar el dominio de la página.
Paso 4: Seleccionar el plan free.
Paso 5: Hacer click en continuar.
Paso 6: Cambiar el nombre del servidor y asignárselo al dominio creado anteriormente.
Paso 7: Hacer click en Continuar.
Paso 8: Esperar a que el nombre del servidor cambie (80 segundos aprox) 

Documentación de certificados de seguridad
El SSL (Security Socket Layer) es un protocolo de seguridad de uso común que establece un canal seguro entre dos ordenadores conectados a través de Internet o de una red interna. En nuestra vida cotidiana, tan dependiente de Internet, solemos comprobar que las conexiones entre un navegador web y un servidor web realizadas a través de una conexión de Internet no segura emplean tecnología SSL. Técnicamente, el protocolo SSL es un método transparente para establecer una sesión segura que requiere una mínima intervención por parte del usuario final.
Paso 1: Ir a la opción crypto en cloudflare 
Paso 2: Seleccionar la opción flexible.
Paso 3: Activar la opción: siempre usar https.
Paso 4: Activar la opción: Reescritura automática HTTPS.
Paso 5: Ir a la opción Page Rules en CloudFlare
Paso 6: Seleccionar la opción: crear page rule.
Paso 7: Introducir el nombre del dominio.
Paso 8: Añadir una configuración y seleccionar: Siempre usar HTTPS
Paso 9: Seleccionar: Save and Deploy.
Plugins intalados
Instalamos really simple en wordpress, luego fuimos a ajustes generales y cambiamos la dirección del sitio de http a https, presionamos ejecutar el plugin y esto ya valida el certificado.
 

El Análisis de vulnerabilidades se realizó de la siguiente manera:
 
 
 
Uno de los plugins utilizados en wordpress(se mencionan más adelante todos los plugins implementados) solucionó el inconveniente que se presenta en el análisis de vulnerabilidad.




Documentación de automatización DevOps
Para la realización la realización de DevOps en el proyecto implementamos jenkins.
Jenkins es un servidor de automatización gratuito y de código abierto . Jenkins ayuda a automatizar el proceso de desarrollo de software , con una integración continua y facilitando los aspectos técnicos de la entrega continua.
Para poder realizar la integración continua de nuestro proyecto, primero se debe lanzar una máquina Ubuntu en AWS e instalar Jenkins en ella, nos conectamos a la instancia por medio del ssh en PUTTY y se siguen los siguientes comandos:
~$ sudo su
~$ wget -q -O — https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add –
~$ sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
~$ sudo apt update
~$ sudo apt install Jenkins
Para iniciar Jenkins se ejecuta el siguiente comando:
~$ sudo systemctl start Jenkins 
Poner a funcionar Jenkins:
Para que Jenkins funcione correctamente debemos activar el puerto 8080, para ello se ejecutan los siguientes comandos:
~$ sudo ufw allow OpenSSH
~$ sudo ufw enable
~$ sudo ufw allow 8080
~$ sudo ufw status








Accedemos a la IP del ec2 en aws y nos debería aparecer lo siguiente:
 
Ya Jenkins se encuentra instalado.
El siguiente paso es realizar la integración continua con el proyecto que se encuentra cargado en github.
Para ellos dentro de la máquina virtual donde tenemos instalado Jenkins, accedemos a la carpeta tmp y clonamos el repositorio: 
git clone https://github.com/damesaa201710054010/proyecto2Telematica.git
Luego, seleccionamos create new jobs en Jenkins:
 
Ingresamos un Item name, seleccionamos alguno de los trabajos disponibles y presionamos OK

 
Si seleccionamos el trabajo freestyle Project, encontraremos el siguiente formulario:

 
Agregamos una descripción, seleccionamos github Project y agregamos la url.

 
Como podemos observar se creó un nuevo trabajo, damos click al ícono del relog para iniciar el trabajo creado.

 
En el panel de control podemos revisar el status, los cambios, las construcciones y acceder al proyecto de github.
Ya podemos realizar la integración continua del proyecto.
Documentación de los servicios utilizados en nube
Máquinas EC2:
Paso 1: Acceder al panel de EC2
Busque EC2 en Compute (Informática) y haga clic para abrir la consola de Amazon EC2.
 
Paso 2: Crear y configurar su máquina virtual
a. Ya está en la consola de Amazon EC2. Haga clic en Launch Instance (Lanzar instancia). 
 
b.  Con Amazon EC2, puede especificar el software y las especificaciones de la instancia que desea utilizar.  
 
________________________________________
c.  Ahora debe elegir un tipo de instancia.  Los tipos de instancias abarcan diversas combinaciones de CPU, memoria, almacenamiento y capacidad de red, por lo que puede elegir la configuración adecuada para sus aplicaciones. Para efectos de este proyecto, seleccionamos t2.micro. Este tipo de instancia se encuentra dentro de la capa gratuita. A continuación, haga clic en Review and Launch (Revisar y lanzar) en la parte inferior de la página.
 

d. Puede examinar las opciones seleccionadas para su instancia, que incluyen los detalles de la AMI, el tipo de instancia, los grupos de seguridad, los detalles de la instancia, el almacenamiento y las etiquetas.   Puede dejar los valores por defecto y hacer clic en Launch (Lanzar) en la parte inferior de la página.
 
Luego creamos el keypair, o seleccionamos uno ya existente, y nos conectamos a la instancia utilizando puttygen para generar una clave privada y putty para conectarse a la instancia mediante la clave privada y la IP de la instancia en AWS.
Instancias creadas en el proyecto:
 

Balanceador de carga:
Un Balanceador de carga fundamentalmente es un dispositivo de software que se pone al frente de un conjunto de servidores que atienden una aplicación y, tal como su nombre lo indica, asigna o balancea las solicitudes que llegan de los clientes a los servidores usando algún algoritmo
Paso 1: Seleccionar un tipo de balanceador de carga
Elastic Load Balancing admite tres tipos de balanceadores de carga: Application Load Balancers, Network Load Balancers y Classic Load Balancers. En este tutorial, va a crear un Classic Load Balancer. Si prefiere crear un Balanceador de carga de aplicaciones, consulte Introducción a los Application Load Balancers en la Guía del usuario de Application Load Balancers. Para crear un balanceador de carga de red, consulte Introducción a los balanceadores de carga de red en la Guía del usuario de los balanceadores de carga de red.
Para crear un Classic Load Balancer
Abra la consola de Amazon EC2 en https://console.aws.amazon.com/ec2/.
En la barra de navegación, elija una región para el balanceador de carga. No olvide seleccionar la misma región que seleccionó para las instancias EC2.
En el panel de navegación, en LOAD BALANCING, elija Load Balancers.
Elija Create Load Balancer.
Para Classic Load Balancer (Balanceador de carga clásico), elija Create (Crear).
Paso 2: Definir el balanceador de carga
Debe proporcionar una configuración básica para el balanceador de carga como, por ejemplo, un nombre, una red y un agente de escucha.
Un agente de escucha es un proceso que comprueba solicitudes de conexión. El agente de escucha se configura con un protocolo y un puerto para las conexiones frontend (entre el cliente y el balanceador de carga) y otro protocolo y otro puerto para las conexiones backend (entre el balanceador de carga y la instancia). En este tutorial, vamos a configurar un agente de escucha que acepta solicitudes HTTP en el puerto 80 y se las envía a las instancias en el puerto 80 a través de HTTP.
Para definir el balanceador de carga y el agente de escucha
En Load Balancer name (Nombre del balanceador de carga), escriba el nombre del balanceador de carga.
El nombre del Classic Load Balancer debe ser único en el conjunto de Classic Load Balancer de la región, puede tener un máximo de 32 caracteres, solo puede contener caracteres alfanuméricos y guiones y no puede comenzar ni finalizar con un guion.
En Create LB inside (Crear balanceador de carga interno), seleccione la misma red que seleccionó para las instancias: EC2-Classic o una VPC específica.
Luego se selecciona la VPC del proyecto y las subredes correspondientes 
 
 
Elija Next: Assign Security Groups (Siguiente: Asignar grupos de seguridad) y añada los grupos de seguridad asociados a la VPC
Elija Next: Configure Security Settings.
Paso 4: Configurar las comprobaciones de estado de las instancias EC2
Elastic Load Balancing comprueba automáticamente el estado de las instancias EC2 registradas en el balanceador de carga. Si Elastic Load Balancing detecta una instancia en mal estado, deja de enviar tráfico a dicha instancia y lo redirecciona a las instancias en buen estado. En este paso, se personalizan las comprobaciones de estado del balanceador de carga.
Para configurar comprobaciones de estado para sus instancias
En la página Configure Health Check (Configurar comprobación de estado), deje Ping Protocol (Protocolo de ping) establecido en HTTP y Ping Port (Puerto de ping) establecido en 80.
En Ping Path, sustituya el valor predeterminado por una barra diagonal sencilla ("/"). Esto le indica a Elastic Load Balancing que envíe consultas de comprobación de estado a la página de inicio predeterminada del servidor web; por ejemplo, index.html.
 
En Advanced Details (Detalles avanzados), deje los valores predeterminados.
Elija Next: Add EC2 Instances (Siguiente: Agregar instancias EC2).
Paso 5: Registrar instancias EC2 con el balanceador de carga
El balanceador de carga distribuye el tráfico entre las instancias que están registradas en el mismo. Al registrar una instancia con una interfaz de red elástica" (ENI), el balanceador de carga direcciona el tráfico a la dirección IP principal de la interfaz principal (eth0) de la instancia. Para registrar instancias EC2 con el balanceador de carga. En la página Add EC2 Instances (Agregar instancias EC2), seleccione las instancias que registrar con su balanceador de carga. Mantenga habilitados el balanceo de carga entre zonas y el vaciado de conexiones.
Balanceadores de carga implementados en el proyecto:
 

VCP:
Amazon Virtual Private Cloud (Amazon VPC) permite aprovisionar una sección de la nube de AWS aislada de forma lógica, en la que puede lanzar recursos de AWS en una red virtual que usted defina. Puede controlar todos los aspectos del entorno de red virtual, incluida la selección de su propio rango de direcciones IP, la creación de subredes y la configuración de tablas de ruteo y gateways de red. Puede usar tanto IPv4 como IPv6 en su VPC para obtener acceso a recursos y aplicaciones de manera segura y sencilla.

Abra la consola de Amazon VPC en https://console.aws.amazon.com/vpc/.
En el panel de navegación, haga clic en VPC Dashboard (Paneles de VPC). Si aún no tiene ningún recurso de VPC, busque el área Your Virtual Private Cloud (Su nube virtual privada) del panel y haga clic en Get started creating a VPC (Empezar a crear una VPC). De lo contrario, haga clic en Start VPC Wizard (Iniciar asistente de VPC).
Seleccione la segunda opción, VPC with a Single Public Subnet (VPC con una sola subred pública) y, a continuación, haga clic en Select (Seleccionar).
Introduzca la siguiente información en el asistente y haga clic en Create VPC (Crear VPC).
IP CIDR block (Bloque CIDR de IP)
10.0.0.0/16
VPC name (Nombre de la VPC)
ADS VPC
Public subnet (Subred pública)
10.0.0.0/24
Availability Zone (Zona de disponibilidad)
No Preference (Sin preferencias)
Subnet name (Nombre de la subred)
ADS Subnet 1
Enable DNS hostnames (Habiliar nombres de host DNS)
Deje la opción predeterminada
Hardware tenancy (Tenencia de hardware)

VCP’s Implementadas en el proyecto:

 

IP elástica:
Las direcciones IP elásticas son direcciones IPv4 estáticas diseñadas para la informática en la nube dinámica. Una dirección IP elástica se asocia a su cuenta de AWS. Con una dirección IP elástica, puede enmascarar los errores de una instancia o software reasignando rápidamente la dirección a otra instancia de su cuenta.
Una dirección IP elástica es una dirección IPv4 pública, a la que se puede tener acceso desde Internet. Si la instancia no tiene una dirección IPv4 pública, puede asociar una dirección IP elástica a la instancia para habilitar la comunicación con Internet. Por ejemplo, esto le permite conectarse a la instancia desde el equipo local.

Abra la consola de Amazon EC2 en https://console.aws.amazon.com/ec2/.
En el panel de navegación, elija Elastic IPs.
Elija Allocate Elastic IP address (Asignar dirección IP elástica).
En Scope (Ámbito), elija VPC o bien EC2-Classic en función del ámbito que se utilizará.
(Solo ámbito de VPC) En Public IPv4 address pool (Grupo de direcciones IPv4 públicas) elija una de las siguientes opciones:
Amazon's pool of IP addresses (Grupo de direcciones IP de Amazon): si desea que una dirección IPv4 se asigne desde un grupo de direcciones IP de Amazon.
My pool of public IPv4 addresses (Mi grupo de direcciones IPv4 públicas): si desea asignar una dirección IPv4 desde un grupo de direcciones IP que ha traído a su cuenta de AWS. Esta opción está deshabilitada si no tiene grupos de direcciones IP.
Elija Allocate.

Elastics IP implementas en el proyecto:

 

RDS:
Paso 1: Crear una instancia de base de datos MySQL
En este paso, utilizaremos Amazon RDS para crear una instancia de base de datos MySQL con una instancia de base de datos de clase db.t2.micro, con backups automatizados activados con un periodo de retención de un día.

a. En la esquina superior derecha de la consola de Amazon RDS, seleccione la región en la que desea crear la instancia de base de datos.
 

b.   En la sección Create database (Crear una base de datos), seleccione Create database.
 
 
 

c.  Ahora dispone de varias opciones de motor.  Para este tutorial, haga clic en el ícono de MySQL, seleccione Only enable options eligible for RDS Free Usage Tier (Permitir solo opciones elegibles para la capa de uso gratuita de RDS) y luego haga clic en Next (Siguiente).
 
 

d. Ahora debe configurar su instancia de base de datos. Haga clic en Next (Siguiente).
 

 

e. Ahora se encuentra en la página de configuración avanzada, donde puede proporcionar información adicional que RDS necesita para implementar la instancia de base de datos MySQL. Haga clic en Create database (Crear base de datos).
f. Se está creando su instancia de base de datos.  Haga clic en View Your DB Instances (Ver sus instancias de base de datos).
La nueva instancia de base de datos aparece en la lista de instancias de base de datos en la consola de RDS. La instancia de base de datos se encontrará en estado creating (creándose) hasta que esté creada y lista para utilizar.  Cuando el estado cambie a available (disponible), podrá conectarse a una base de datos de la instancia de base de datos.  Si lo desea, puede pasar al siguiente paso mientras espera a que la instancia de base de datos esté disponible.
 

Bases de datos implementadas en el proyecto:

 

S3:
Para implementar S3 en el proyecto, creamos una cuenta con los servicios gratuitos de aws que está asociada al correo proyectotelematica@outlook.com
Esta cuenta da acceso a 5 gigas gratis de almacenamiento.
Se creó un Bucket llamado wordpresstelematic, ubicado al norte de california. En los permisos solo le dimos acceso a wordpress.

 
Para realizar la integración con wordpress se realiza mediante un plugin(se explica más adelante).
S3 en wordpress:
 
CloudFlare:
CloudFlare es un sistema gratuito que actúa como un proxy (intermediario) entre los visitantes del sitio y el servidor. Al actuar como un proxy, CloudFlare guarda temporalmente contenido estático del sitio, el cual disminuye el número de peticiones al servidor pero sigue permitiendo a los visitantes el acceso al sitio.
Pagerules: sirve para direccionar todas las páginas que utilicen el dominio con http a https.

 

Caching, sistema que provee los datos de la página desde el servidor más cercano hasta los usuarios(cdn)

 
Se implementó autominify,esto permite compactar el código para mejorar el rendimiento de la aplicación.

 
Rocket Loader, también permite mejorar el rendimiento de la aplicación.

 

Configuraciones de CloudFlare:

 

 

 

 

Recaptcha:
Para el recaptcha se usó googleRecaptcha. Añadimos un nuevo sitio, llenamos los datos del dominio, seleccionamos el tipo de catpcha, guardamos los cambios y se generan unas claves, y las claves se colocan en el plugin de wordpress.

 

 
Facebook 
Para la implementación de Facebook para el inicio de sesión, se crea una cuenta de desarrollador en Facebook, en configuración se le agrega una uri de redireccionamiento proporcionada por el plugin de wordpress, se guardan los cambios y en configuración de información básica se llenan los datos del dueño y se guardan los cambios, allí se proporciona un id de la aplicación y una clave secreta, que son proporcionados al plugin de wordpress, luego a ese producto se le añade iniciar sesión con facebook y se le asocia el dominio.

 

 




Análisis de Costo de la solución.  Inversión inicial y mensual.
Costo inicial de la aplicación: 80 dólares.
Aproximadamente se cobra por hora de instancia de bases de datos 3 dólares.
Costo mensual de la instancia de base de datos= 3*24*30 = 2160 dólares.
La instancia EC2 cobra aproximadamente 0.102 centavos de dólar, de utilización por hora.
Costo mensual de la instancia EC2= 0.102*24*30= 73.44 dólares.
La inversión mensual sería aproximadamente de: 2233,44 dólares.

Documentación de monitoreo y gestión.

Amazon CloudWatch es un servicio de monitorización y administración que suministra datos e información procesable para aplicaciones y recursos de infraestructura locales, híbridos y de AWS. Con CloudWatch, puede recopilar y obtener acceso a todos los datos de rendimiento y operaciones en formato de registros y métricas a partir de una sola plataforma. Esto le permite superar el desafío de monitorear aplicaciones y sistemas individuales aislados (servidor, red, base de datos, etc.). CloudWatch le permite monitorear una pila completa (aplicaciones, infraestructura y servicios) y utilizar alarmas, registros y datos de eventos para tomar acciones automatizadas y disminuir el tiempo de resolución (MTTR). Esto libera recursos importantes y le permite enfocarse en la creación de aplicaciones y valor comercial.
Creación de un panel de CloudWatch
Para comenzar a utilizar los paneles de CloudWatch, primero debe crear un panel. Puede crear varios paneles. El número de paneles de CloudWatch en su cuenta de AWS es ilimitado. Todos los paneles son globales, no específicos de cada región.
En esta sección, se describen los pasos para crear un panel a través de la consola. También puede crear un panel con la API PutDashboard, que utiliza una cadena JSON para definir el contenido del panel. Para crear un panel mediante PutDashboard y basar este panel en un panel existente, elija Actions (Acciones) y después View/edit source (Ver/editar código fuente) para mostrar y copiar la cadena JSON de un panel actual y utilizarla para su nuevo panel.
Para obtener más información sobre cómo crear un panel con la API, consulte PutDashboard en la Amazon CloudWatch API Reference.
Para crear un panel con la consola
Abra la consola de CloudWatch en https://console.aws.amazon.com/cloudwatch/.
En el panel de navegación, seleccione Dashboards (Paneles) y después Create dashboard (Crear panel).
En el cuadro de diálogo Create new dashboard (Crear nuevo panel), escriba un nombre para el panel y seleccione Create dashboard (Crear panel).
Si utiliza el nombre CloudWatch-Default, el panel aparece en la información general de la página de inicio de CloudWatch. Para obtener más información, consulte Introducción a Amazon CloudWatch.
Si utiliza grupos de recursos y asigna al panel el nombre CloudWatch-Default:ResourceGroupName, aparece en la página de inicio de CloudWatch cuando se centre en ese grupo de recursos.
En el cuadro de diálogo Add to this dashboard, realice una de las acciones siguientes:
Para agregar un gráfico a su panel, elija Line (Línea) o Stacked area (Área apilada) y seleccione Configure (Configurar). En el cuadro de diálogo Add metric graph (Añadir gráfico de métricas), seleccione las métricas que desea representar gráficamente y, a continuación, elija Create widget (Craer widget). Si una métrica específica no aparece en el cuadro de diálogo porque no ha publicado datos durante más de 14 días, puede agregarla manualmente. Para obtener más información, consulte Representar gráficamente métricas en un panel de CloudWatch de forma manual.
Para agregar al panel un número que muestre la métrica, seleccione Number (Número) y después Configure (Configurar). En el cuadro de diálogo Add metric graph (Añadir gráfico de métricas), seleccione las métricas que desea representar gráficamente y, a continuación, elija Create widget (Craer widget).
Para agregar un bloque de texto al panel, elija Text (Texto) y después Configure (Configurar). En el cuadro de diálogo New text widget (Nuevo widget de texto), para Markdown (Marcado), agregue texto y dele formato utilizando Markdown (Marcado). Elija Create widget.
Si lo prefiere, seleccione Add widget y repita el paso 4 para agregar otro widget al panel. Puede repetir este paso varias veces.
Elija Save dashboard.
Puede editar una alarma existente y actualizar la lista de notificaciones de correo electrónico de Amazon SNS que utiliza.
CloudWatch ha cambiado la interfaz de usuario de alarmas. De forma predeterminada, se muestra la nueva interfaz de usuario, pero puede elegir volver a la interfaz de usuario antigua. Este tema contiene pasos para cada uno de ellas.
Para editar una alarma mediante la nueva interfaz de usuario de alarmas
1.	Abra la consola de CloudWatch en https://console.aws.amazon.com/cloudwatch/.
2.	En el panel de navegación, elija Alarms (Alarmas).
3.	Elija el nombre de la alarma.
4.	Elija Edit (Editar).
Aparece la página Specify metric and conditions (Especificar métrica y condiciones), que muestra un gráfico y otra información sobre la métrica y la estadística que ha seleccionado.
5.	Para cambiar la métrica, elija Edit (Editar), elija la pestaña All metrics (Todas las métricas) y realice una de las siguientes operaciones:
•	Elija el espacio de nombres del servicio que contiene la métrica que desea. Continúe eligiendo opciones conforme aparezcan para delimitar las opciones. Cuando aparezca una lista de métricas, active la casilla de verificación situada junto a la que desee utilizar.
•	En el campo de búsqueda, escriba el nombre de una métrica, dimensión o ID de recurso y pulse Intro. A continuación, elija uno de los resultados y continúe hasta que se muestre una lista de métricas. Seleccione la casilla de verificación situada junto a la métrica que desee.
Elija Select metric (Seleccionar métrica).
6.	Para cambiar otros aspectos de la alarma, elija las opciones apropiadas. Para cambiar la cantidad de puntos de datos que deben estar fuera del umbral de la alarma para pasar al estado ALARM o para modificar la forma en que se tratan los datos que faltan, elija Additional configuration (Configuración adicional).
7.	Seleccione Next (Siguiente).
8.	En Notification (Notificación), Auto Scaling action (Acción de Auto Scaling) y EC2 action (Acción de EC2), edite, si lo desea, las acciones que se realizarán cuando se active la alarma A continuación, elija Next (Siguiente).
9.	También puede cambiar la descripción de la alarma.
No puede cambiar el nombre de una alarma existente. Puede copiar la alarma y asignar un nombre diferente a la nueva alarma. Para copiar una alarma, seleccione la casilla de verificación situada junto al nombre de la alarma en la lista de alarmas y elija Action (Acción), Copy (Copiar).
10.	Seleccione Next (Siguiente).
11.	En Preview and create (Obtener vista previa y crear), confirme que la información y las condiciones son las que desea y, a continuación, elija Update alarm (Actualizar alarma).
Para editar una alarma con la interfaz de usuario de alarmas anterior
1.	Abra la consola de CloudWatch en https://console.aws.amazon.com/cloudwatch/.
2.	En el panel de navegación, elija Alarms (Alarmas).
3.	Seleccione la alarma y elija Actions (Acciones), Modify (Modificar).
4.	En la página Modify Alarm (Modificar alarma), actualice la alarma según sea necesario y elija Save Changes (Guardar cambios). Para modificar la expresión, las métricas, el periodo o la estadística, en primer lugar, elija Edit (Editar) cerca de la parte superior de la pantalla.
No puede cambiar el nombre de una alarma existente. Puede cambiar la descripción. O bien puede copiar la alarma y asignar un nombre diferente a la nueva alarma. Para copiar una alarma, selecciónela y, a continuación, elija Actions (Acciones), Copy (Copy).
Para actualizar una lista de notificación por correo electrónico que se creó utilizando la consola de Amazon SNS
1.	Abra la consola de Amazon SNS en https://console.aws.amazon.com/sns/v3/home/.
2.	En el panel de navegación, elija Topics (Temas) y, a continuación, seleccione el ARN de su lista de notificación (tema).
3.	Aplique alguna de las siguientes acciones:
•	Para añadir una dirección de correo electrónico, elija Create subscription. En Protocol (Protocolo), elija Email (Correo electrónico). En Endpoint (Punto de enlace), escriba la dirección de correo electrónico del nuevo destinatario. Seleccione Create subscription (Crear suscripción).
•	Para eliminar una dirección de correo electrónico, elija el Subscription ID. Elija Other subscription actions, Delete subscriptions.
4.	Elija Publish to topic (Publicar en tema)



Documentación de recuperación ante desastres.  (Backups, Restore)

Como tenemos dos instancias, tenemos la posibilidad de que el servicio no sea interrumpido, las instancias se encuentran en regiones diferentes de estados unidos porque AWS, no permite crear instancias fuera de estados unidos.
Backup manual de la base de datos.

 
Además, la base de datos está configurada para que se realice un backup de los datos cada 7 días

 




PLUGINS INTALADOS EN WORDPRESS PARA LA REALIZACIÓN DEL PROYECTO:
 
El primer plugin, utiliza los servicios de Google para poner un recapcha en los formularios de inicio de sesión.
El segundo plugin, realiza una revisión general de la seguridad del sistema, la fue revisión fue exitosa.
 
El tercer plugin, verifica que no haya basura en los comentarios (que no introduzcan enlaces que puedan dañar la base de datos por ejemplo)
El cuarto plugin, permite realizar el inicio de sesión con terceros:
 
Como se puede observar en la imagen, solo implementamos inicio y registro de sesión usando terceros con facebook, mediante la cuenta de desarrollador de Facebook.
El quinto plugin, permite que se integre el sistema con la aplicación de Google authentication.
 
Se permite leer un código QR con la aplicación, y en cada inicio de sesión en el block se pide un código que se muestra en la aplicación y que cambia cada tres minutos
El sexto plugin, Permite analizar las ip que tienen acceso a la página, por lo tanto puede ser entrenado durante varios días para que identifique las ip recurrentes para que sea más efectivo, además ayuda a bloquear ataques.
 
El séptimo plugin, permite la gestión de envío y recepción de correos electrónicos, esto permitió habilitar las funciones de registrarse y recuperar contraseña, debido a que no se poseía un host de correo electrónico utilizamos los servidores de Microsoft con la cuneta proyetotelematica@outlook. 
El octavo plugin, permite hacer la integración con s3 de aws, para realizar la carga de objetos que no sean almacenados en el servidor.
  

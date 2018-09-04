---
title: Creación de servidores vinculados (motor de base de datos de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2015
ms.prod: sql
ms.prod_service: database-engine
ms.component: linked-servers
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.linkedserver.properties.general.f1
- sql13.swb.linkedserver.properties.security.f1
- sql13.swb.linkedserver.properties.provider.f1
- sql13.swb.linkedserver.properties.options.f1
helpviewer_keywords:
- linked servers [SQL Server], creating
ms.assetid: 3228065d-de8f-4ece-a9b1-e06d3dca9310
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1cf471808826acbfb8a5574b78a870fce8d8ab30
ms.sourcegitcommit: 2a47e66cd6a05789827266f1efa5fea7ab2a84e0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/31/2018
ms.locfileid: "43348236"
---
# <a name="create-linked-servers-sql-server-database-engine"></a>Crear servidores vinculados (motor de base de datos de SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
 > Para obtener contenido relacionado con versiones anteriores de SQL Server, vea [Crear servidores vinculados (motor de base de datos de SQL Server)](create-linked-servers-sql-server-database-engine.md).

  En este tema se muestra cómo crear un servidor vinculado y tener acceso a los datos desde otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. La creación de un servidor vinculado permite trabajar con datos de varios orígenes. El servidor vinculado no necesita ser otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], sino que es un escenario común.  
  
##  <a name="Background"></a> Información previa  
 Un servidor vinculado permite obtener acceso a consultas heterogéneas distribuidas en orígenes de datos OLE DB. Después de crear un servidor vinculado, las consultas distribuidas se pueden ejecutar en este servidor. Las consultas pueden unir tablas de varios orígenes de datos. Si el servidor vinculado se define como una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se pueden ejecutar procedimientos almacenados remotos.  
  
 Las capacidades y los argumentos requeridos de los servidores vinculados pueden variar significativamente. Los ejemplos de este tema proporcionan un ejemplo típico. Sin embargo, no se describen todas las opciones. Para obtener más información, vea [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).  
  
##  <a name="Security"></a> Seguridad  
  
### <a name="permissions"></a>Permisos  
 Cuando se usan instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] , se requiere el permiso **ALTER ANY LINKED SERVER** en el servidor o la pertenencia al rol fijo de servidor **setupadmin** . Cuando se usa [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] , se requiere el permiso **CONTROL SERVER** o la pertenencia al rol fijo de servidor **sysadmin** .  
  
##  <a name="Procedures"></a> Crear un servidor vinculado  
 Puede usar cualquiera de los elementos siguientes:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
##### <a name="to-create-a-linked-server-to-another-instance-of-sql-server-using-sql-server-management-studio"></a>Para crear un servidor vinculado a otra instancia de SQL Server utilizando SQL Server Management Studio  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra el Explorador de objetos, expanda **Objetos de servidor**, haga clic con el botón derecho en **Servidores vinculados**y, luego, haga clic en **Nuevo servidor vinculado**.  
  
2.  En el cuadro **Servidor vinculado** de la página **General** , escriba el nombre de la instancia de **SQL Server** al que esté vinculando.  
  
     **SQL Server**  
     Identifica el servidor vinculado como una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si usa este método para definir un servidor vinculado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el nombre especificado en **Servidor vinculado** debe ser el nombre de red del servidor. Además, cualquier tabla obtenida del servidor pertenecerá a la base de datos predeterminada definida para el inicio de sesión del servidor vinculado.  
  
     **Otro origen de datos**  
     Especifique un tipo de servidor OLE DB distinto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Al hacer clic en esta opción, se activan las opciones que aparecen debajo.  
  
     **Proveedor**  
     Seleccione un origen de datos OLE DB del cuadro de lista. El proveedor OLE DB se ha registrado con el PROGID especificado en el registro.  
  
     **Nombre del producto**  
     Escriba el nombre del producto del origen de datos OLE DB para agregarlo como servidor vinculado.  
  
     **Origen de datos**  
     Escriba el nombre del origen de datos como lo interpreta el proveedor OLE DB. Si se está conectando a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], proporcione el nombre de instancia.  
  
     **Cadena de proveedor**  
     Escriba el identificador de programación (PROGID) único del proveedor OLE DB que corresponde al origen de datos. Para ver ejemplos de cadenas de proveedores válidas, vea [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).  
  
     **Ubicación**  
     Escriba la ubicación de la base de datos según la interpretación del proveedor OLE DB.  
  
     **Catálogo**  
     Escriba el nombre del catálogo que se va a usar cuando se establezca la conexión al proveedor OLE DB.  
  
     Para comprobar la capacidad de conexión a un servidor vinculado, en el Explorador de objetos, haga clic con el botón derecho en el servidor vinculado y, luego, haga clic en **Probar conexión**.  
  
    > [!NOTE]  
    >  Si la instancia de **SQL Server** es la instancia predeterminada, escriba el nombre del equipo que hospede la instancia de **SQL Server**. Si **SQL Server** es una instancia con nombre, escriba el nombre del equipo y el de la instancia, por ejemplo, **Accounting\SQLExpress**.  
  
3.  En el área **Tipo de servidor** , seleccione **SQL Server** para indicar que el servidor vinculado es otra instancia de **SQL Server**.  
  
4.  En la página **Seguridad** , especifique el contexto de seguridad que se usará cuando la versión original de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conecte con el servidor vinculado. En un entorno de dominio donde los usuarios se conectan mediante sus inicios de sesión, la selección de **Se establecerán usando el contexto de seguridad actual del inicio de sesión** suele ser la mejor opción. Cuando los usuarios se conecten a la versión original de **SQL Server** usando un inicio de sesión de **SQL Server** , la mejor opción suele ser seleccionar **Se establecerán usando este contexto de seguridad**y, a continuación, proporcionar las credenciales necesarias para la autenticación en el servidor vinculado.  
  
     **Inicio de sesión local**  
     Permite especificar el inicio de sesión local que se puede conectar al servidor vinculado. El inicio de sesión local puede ser un inicio de sesión que utilice la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un inicio de sesión de autenticación de Windows. Utilice esta lista para restringir la conexión a inicios de sesión específicos o para permitir que algunos inicios de sesión se conecten como un inicio de sesión diferente.  
  
     **Impersonate**  
     Pasa el nombre de usuario y la contraseña del inicio de sesión local al servidor vinculado. En la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe existir un inicio de sesión con el mismo nombre y contraseña en el servidor remoto. En los inicios de sesión de Windows, el inicio de sesión debe ser un inicio de sesión válido en el servidor vinculado.  
  
     Para utilizar la suplantación, la configuración debe cumplir los requisitos de la delegación.  
  
     **Usuario remoto**  
     Use el usuario remoto para asignar usuarios no definidos en **Inicio de sesión local**. El **Usuario remoto** debe ser un inicio de sesión de autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el servidor remoto.  
  
     **Contraseña remota**  
     Permite especificar la contraseña del usuario remoto.  
  
     **Agregar**  
     Permite agregar un nuevo inicio de sesión local.  
  
     **Quitar**  
     Quita un inicio de sesión local existente.  
  
     **No se establecerán**  
     Permite especificar que no se establecerán conexiones para los inicios de sesión que no estén definidos en la lista.  
  
     **Se establecerán sin usar un contexto de seguridad**  
     Permite especificar que se establecerán conexiones sin utilizar un contexto de seguridad para los inicios de sesión no definidos en la lista.  
  
     **Se establecerán usando el contexto de seguridad actual del inicio de sesión**  
     Permite especificar que se establecerá una conexión con el contexto de seguridad actual del inicio de sesión para los inicios de sesión no definidos en la lista. Si está conectado al servidor local mediante la autenticación de Windows, las credenciales de Windows se utilizarán para conectar al servidor remoto. Si está conectado al servidor local mediante la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , la contraseña y el nombre de usuario de inicio de sesión se utilizarán para conectar al servidor remoto. En este caso, debe existir un inicio de sesión con el mismo nombre y contraseña en el servidor remoto.  
  
     **Se establecerán usando este contexto de seguridad**  
     Especifique que se establecerá una conexión con el inicio de sesión y la contraseña especificados en los cuadros **Inicio de sesión remoto** y **Con contraseña** para los inicios de sesión que no estén definidos en la lista. El inicio de sesión remoto debe ser un inicio de sesión de autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el servidor remoto.  
  
5.  Opcionalmente, para ver o especificar opciones de servidor, haga clic en la página **Opciones del servidor**  .  
  
     **Compatible con la intercalación**  
     Afecta a la ejecución de consultas distribuidas en los servidores vinculados. Si esta opción se establece en true, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supone asume que todos los caracteres del servidor vinculado son compatibles con el servidor local en lo que respecta a juego de caracteres y secuencia de intercalación (o criterio de ordenación). Esta opción habilita a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para enviar comparaciones en columnas de caracteres al proveedor. Si no se establece esta opción, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siempre evalúa localmente las comparaciones en las columnas de caracteres.  
  
     Esta opción solo se debe establecer si se tiene la certeza de que el origen de datos correspondiente al servidor vinculado tiene el mismo juego de caracteres y criterio de ordenación que el servidor local.  
  
     **Acceso a datos**  
     Habilita y deshabilita un servidor vinculado para el acceso a consultas distribuidas.  
  
     **RPC**  
     Habilita RPC desde el servidor especificado.  
  
     **RPC fuera**  
     Habilita RPC en el servidor especificado.  
  
     **Usar intercalación remota**  
     Determina si se utilizará la intercalación de una columna remota o de un servidor local.  
  
     Si es true, para los orígenes de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se utilizará la intercalación de columnas remotas, y la intercalación especificada en el nombre de la intercalación se utilizará para los orígenes de datos que no sean de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     Si es false, las consultas distribuidas siempre utilizarán la intercalación predeterminada del servidor local, mientras que el nombre de intercalación y la intercalación de columnas remotas se pasarán por alto. El valor predeterminado es false.  
  
     **Nombre de intercalación**  
     Especifica el nombre de la intercalación que ha utilizado el origen de datos remoto si Usar intercalación remota es true y el origen de datos no es de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El nombre debe pertenecer a una de las intercalaciones que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]admite.  
  
     Utilice esta opción cuando se obtenga acceso a un origen de datos OLE DB que no sea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], pero que tenga una intercalación que coincida con una de las intercalaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     El servidor vinculado debe permitir el uso de una única intercalación para todas las columnas de ese servidor. No establezca esta opción si el servidor vinculado admite varias intercalaciones dentro de un único origen de datos o si no se puede determinar si la intercalación del servidor vinculado coincide con alguna de las intercalaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     **Tiempo de espera de la conexión**  
     Valor del tiempo de espera en segundos para conectarse a un servidor vinculado.  
  
     Si es 0, use el valor de la opción **Tiempo de espera de inicio de sesión remoto** predeterminado [sp_configure](../../database-engine/configure-windows/configure-the-remote-login-timeout-server-configuration-option.md) .  
  
     **Tiempo de espera de la consulta**  
     Valor del tiempo de espera en segundos para las consultas que se realizan en un servidor vinculado.  
  
     Si es 0, use el valor de la opción **Tiempo de espera de consulta remota** predeterminado [sp_configure](../../database-engine/configure-windows/configure-the-remote-query-timeout-server-configuration-option.md) .  
  
     **Habilitar promoción de transacciones distribuidas**  
     Use esta opción para proteger las acciones de un procedimiento entre servidores a través de una transacción del Coordinador de transacciones distribuidas de [!INCLUDE[msCoName](../../includes/msconame-md.md)] (MS DTC). Cuando esta opción es TRUE, al llamar a un procedimiento remoto almacenado se inicia una transacción distribuida y se da de alta en MS DTC. Para obtener más información, vea [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md).  
  
6.  Haga clic en **Aceptar**.  
  
##### <a name="to-view-the-provider-options"></a>Para ver las opciones de proveedor  
  
-   Para ver las opciones que el proveedor pone disponibles, haga clic en la página **Opciones de proveedor** .  
  
     Todos los proveedores no tienen las mismas opciones disponibles. Por ejemplo, algunos tipos de datos tienen índices disponibles y otros pueden no tenerlos. Utilice este cuadro de diálogo para que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueda conocer mejor las capacidades del proveedor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala algunos proveedores de datos comunes; con todo, cuando cambia el producto que proporciona los datos, el proveedor instalado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podría no admitir todas las características más recientes. La mejor fuente de información sobre las capacidades del producto que proporciona los datos es la documentación del producto.  
  
     **Parámetro dinámico**  
     Indica que el proveedor permite la sintaxis de marcador de parámetro '?' para consultas con parámetros. Establezca esta opción solo si el proveedor admite la interfaz **ICommandWithParameters** y  '?’ como marcador de parámetro. Si establece esta opción, permitirá a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecutar consultas con parámetros en el proveedor. La capacidad de ejecutar consultas con parámetros en el proveedor puede mejorar el rendimiento de determinadas consultas.  
  
     **Consultas anidadas**  
     Indica que el proveedor permite instrucciones `SELECT` anidadas en la cláusula FROM. Si establece esta opción, permitirá a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] delegar en el proveedor determinadas consultas que precisan anidar instrucciones SELECT en la cláusula FROM.  
  
     **Solo nivel cero**  
     Solo se invocan interfaces OLE DB de nivel 0 en el proveedor.  
  
     **Permitir en proceso**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite crear una instancia del proveedor como un servidor en proceso. Si no se establece esta opción, el comportamiento predeterminado consiste en crear una instancia del proveedor fuera del proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La creación de instancias del proveedor fuera del proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] protege el proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de posibles errores en el proveedor. Si se crea una instancia del proveedor fuera del proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , no se permitirán actualizaciones ni inserciones que hagan referencia a columnas long (**text**, **ntext**o **image**).  
  
     **Actualizaciones no realizadas**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite realizar actualizaciones, aunque **ITransactionLocal** no esté disponible. Si esta opción está habilitada, no podrá recuperar las actualizaciones en el proveedor, ya que éste no admite transacciones.  
  
     **Índice como ruta de acceso**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tratará de usar los índices del proveedor para capturar los datos. De forma predeterminada, los índices solo se utilizan para metadatos y nunca se abren  
  
     **Denegar el acceso ad hoc**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no permite el acceso ad hoc mediante las funciones OPENROWSET y OPENDATASOURCE en el proveedor OLE DB. Si no se establece esta opción, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tampoco permite el acceso ad hoc.  
  
     **Admite el operador LIKE**  
     Indica que el proveedor admite consultas mediante la palabra clave LIKE.  
  
###  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Para crear un servidor vinculado mediante [!INCLUDE[tsql](../../includes/tsql-md.md)], use las instrucciones [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md) y [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md).  
  
##### <a name="to-create-a-linked-server-to-another-instance-of-sql-server-using-transact-sql"></a>Para crear un servidor vinculado a otra instancia de SQL Server con Transact-SQL  
  
1.  En el Editor de consultas, escriba el siguiente comando [!INCLUDE[tsql](../../includes/tsql-md.md)] para vincular a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] llamada `SRVR002\ACCTG`:  
  
    ```sql  
    USE [master]  
    GO  
    EXEC master.dbo.sp_addlinkedserver   
        @server = N'SRVR002\ACCTG',   
        @srvproduct=N'SQL Server' ;  
    GO  
  
    ```  
  
2.  Ejecute el siguiente código para configurar el servidor vinculado con el fin de que use las credenciales de dominio del inicio de sesión que usa el servidor vinculado.  
  
    ```sql  
    EXEC master.dbo.sp_addlinkedsrvlogin   
        @rmtsrvname = N'SRVR002\ACCTG',   
        @locallogin = NULL ,   
        @useself = N'True' ;  
    GO  
  
    ```  
  
##  <a name="FollowUp"></a> Seguimiento: pasos que se deben realizar después de crear un servidor vinculado  
  
#### <a name="to-test-the-linked-server"></a>Para probar el servidor vinculado  
  
-   Ejecute el siguiente código para probar la conexión al servidor vinculado. En este ejemplo se devuelven los nombres de las bases de datos del servidor vinculado.  
  
    ```sql  
    SELECT name FROM [SRVR002\ACCTG].master.sys.databases ;  
    GO  
  
    ```  
  
#### <a name="writing-a-query-that-joins-tables-from-a-linked-server"></a>Escribir una consulta que una tablas desde un servidor vinculado  
  
-   Use nombres de cuatro partes para hacer referencia a un objeto de un servidor vinculado. Ejecute el código siguiente para que se devuelva una lista de todos los inicios de sesión del servidor local y sus inicios de sesión coincidentes en el servidor vinculado.  
  
    ```sql  
    SELECT local.name AS LocalLogins, linked.name AS LinkedLogins  
    FROM master.sys.server_principals AS local  
    LEFT JOIN [SRVR002\ACCTG].master.sys.server_principals AS linked  
        ON local.name = linked.name ;  
    GO  
    ```  
  
     Cuando se devuelve NULL para el inicio de sesión del servidor vinculado, se indica que el inicio de sesión no existe en el servidor vinculado. Estos inicios de sesión no podrán usar el servidor vinculado a menos que este se configure para pasar un contexto de seguridad distinto o el servidor vinculado acepte conexiones anónimas.  
  
## <a name="see-also"></a>Ver también  
 [Servidores vinculados &#40;motor de base de datos&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)  
  
  

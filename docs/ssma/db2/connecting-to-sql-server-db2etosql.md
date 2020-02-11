---
title: Conexión a SQL Server (DB2eToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: b59803cb-3cc6-41cc-8553-faf90851410e
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 7ab4c1f691820fb19dde7a3e3166abc2ff065b18
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68126643"
---
# <a name="connecting-to-sql-server-db2etosql"></a>Conexión a SQL Server (DB2eToSQL)
Para migrar las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012, 2014 o a Azure SQL dB, debe conectarse a cualquiera de estas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]instancias de destino de. Cuando se conecta, SSMA obtiene los metadatos de todas las bases de datos de la instancia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de y muestra los metadatos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la base de datos en el explorador de metadatos. SSMA almacena información acerca de la instancia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de a la que está conectado, pero no almacena contraseñas.  
  
La conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permanece activa hasta que se cierra el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si desea una conexión activa con el servidor. Puede trabajar sin conexión hasta que cargue los objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos en y migre los datos.  
  
Los metadatos de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia de no se sincronizan automáticamente. En su lugar, para actualizar los metadatos en el explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadatos, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe actualizar manualmente los metadatos. Para obtener más información, vea la sección [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "sincronizar metadatos" más adelante en este tema.  
  
## <a name="required-sql-server-permissions"></a>Permisos SQL Server necesarios  
La cuenta que se usa para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requiere permisos diferentes en función de las acciones que realiza la cuenta:  
  
-   Para convertir objetos DB2 en [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxis, actualizar metadatos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o guardar la sintaxis convertida en scripts de, la cuenta debe tener permiso para iniciar sesión en la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]instancia de.  
  
-   Para cargar los objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]base de datos en, la cuenta debe ser miembro del rol de servidor **sysadmin** . Esto es necesario para instalar ensamblados CLR.  
  
-   Para migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la cuenta debe ser miembro del rol de servidor **sysadmin** . Esto es necesario para ejecutar los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] paquetes de migración de datos del agente.  
  
-   Para ejecutar el código generado por SSMA, la cuenta debe tener permisos de **ejecución** para todas las funciones definidas por el usuario en el esquema de **ssma_DB2** de la base de datos de destino. Estas funciones proporcionan una funcionalidad equivalente de las funciones del sistema DB2 y las usan los objetos convertidos.  
  
Si la cuenta que se usa para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es realizar todas las tareas de migración, la cuenta debe ser miembro del rol de servidor **sysadmin** .  
  
## <a name="establishing-a-sql-server-connection"></a>Establecer una conexión SQL Server  
Antes de convertir los objetos de base [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de datos DB2 en sintaxis, debe establecer una conexión con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la instancia de en la que desea migrar la base de datos o bases de datos DB2.  
  
Al definir las propiedades de conexión, también se especifica la base de datos en la que se migrarán los objetos y los datos. Puede personalizar esta asignación en el nivel de esquema de DB2 después de conectarse [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]a. Para obtener más información, vea [asignar esquemas DB2 a esquemas de SQL Server &#40;&#41;DB2ToSQL ](../../ssma/db2/mapping-db2-schemas-to-sql-server-schemas-db2tosql.md).  
  
> [!IMPORTANT]  
> Antes de intentar conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], asegúrese de que la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se está ejecutando y puede aceptar conexiones.  
  
**Para conectarse a SQL Server**  
  
1.  En el menú **archivo** , seleccione **conectarse a SQL Server**.  
  
    Si anteriormente se conectó a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el nombre del comando se volverá **a conectar a SQL Server**.  
  
2.  En el cuadro de diálogo conexión, escriba o seleccione el nombre de la instancia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de.  
  
    -   Si se está conectando a la instancia predeterminada en el equipo local, puede especificar **localhost** o un punto (**.**).  
  
    -   Si se va a conectar a la instancia predeterminada en otro equipo, escriba el nombre del equipo.  
  
    -   Si se va a conectar a una instancia con nombre en otro equipo, escriba el nombre del equipo seguido de una barra diagonal inversa y, a continuación, el nombre de la instancia, como MyServer\MyInstance.  
  
3.  Si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está configurada para aceptar conexiones en un puerto no predeterminado, escriba el número de puerto que se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza para las conexiones en el cuadro **Puerto del servidor** . Para la instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el número de puerto predeterminado es 1433. En el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] caso de las instancias con nombre, SSMA intentará obtener el número de puerto del servicio explorador.  
  
4.  En el cuadro **base de datos** , escriba el nombre de la base de datos de destino.  
  
    Esta opción no está disponible cuando se vuelve a conectar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]a.  
  
5.  En el cuadro **autenticación** , seleccione el tipo de autenticación que se utilizará para la conexión. Para usar la cuenta de Windows actual, seleccione **autenticación de Windows**. Para usar un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión, seleccione **SQL Server autenticación**y proporcione el nombre de inicio de sesión y la contraseña.  
  
6.  Para una conexión segura, se agregan dos controles, las casillas de verificación **cifrar conexión** y **TrustServerCertificate** . Solo cuando se activa **cifrar conexión** , la casilla **TrustServerCertificate** está visible. Cuando se activa la opción **cifrar conexión** (true) y **TrustServerCertificate** está desactivado (false), se validará el certificado SSL SQL Server. Validar el certificado de servidor es una parte del protocolo de enlace de SSL y asegurarse de que el servidor es el apropiado al que hay que conectarse. Para garantizar esto, se debe instalar un certificado en el lado cliente y en el lado servidor.  
  
7.  Haga clic en **Conectar**.  
  
**Compatibilidad con versiones posteriores**  
  
-   Podrá conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 y 2012 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 cuando el proyecto de migración creado sea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
-   Podrá conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 y 2014 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 cuando el proyecto de migración creado sea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, pero no podrá conectarse a las versiones anteriores, es decir, a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
-   Podrá conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 cuando el proyecto creado sea SQL Server 2012.  
  
||||||  
|-|-|-|-|-|  
|**VERSIÓN de tipo de proyecto frente al servidor de destino**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012 <br />(Versión: 11. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 <br />(Versión: 12. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016 <br />(Versión: 13. x)|Azure SQL DB|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012|Sí|Sí|Sí||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014||Sí|Sí||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014|||Sí||  
|Azure SQL DB||||Sí|  
  
> [!IMPORTANT]  
> La conversión de los objetos de base de datos se realiza según el tipo de proyecto, pero no según la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versión de a la que esté conectado. En el caso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 2012 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , 2014 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , 2016 o Azure SQL dB.  
  
## <a name="synchronizing-sql-server-metadata"></a>Sincronizar metadatos de SQL Server  
Los metadatos acerca de las bases de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos no se actualizan automáticamente. Los metadatos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del explorador de metadatos son una instantánea de los metadatos al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]conectarse por primera vez a o la última vez que se actualizaron los metadatos manualmente. Puede actualizar manualmente los metadatos de todas las bases de datos o de cualquier base de datos o objeto de base de datos.  
  
**Para sincronizar los metadatos**  
  
1.  Asegúrese de que está conectado a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el explorador de metadatos, active la casilla situada junto a la base de datos o el esquema de la base de datos que desea actualizar.  
  
    Por ejemplo, para actualizar los metadatos de todas las bases de datos, active la casilla situada junto a **bases**de datos.  
  
3.  Haga clic con el botón derecho en **bases**de datos o en el esquema de base de datos o de base de datos individual y seleccione **sincronizar con base de datos**.  
  
## <a name="next-step"></a>siguiente paso  
El siguiente paso de la migración depende de las necesidades del proyecto:  
  
-   Para personalizar la asignación entre esquemas y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bases de datos de DB2, consulte asignación de [esquemas DB2 a esquemas de SQL Server &#40;&#41;DB2ToSQL ](../../ssma/db2/mapping-db2-schemas-to-sql-server-schemas-db2tosql.md).  
  
-   Para personalizar las opciones de configuración de los proyectos, vea [configuración del proyecto &#40;conversión&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-conversion-db2tosql.md) y secciones relacionadas.  
  
-   Para personalizar la asignación de los tipos de datos de origen y de destino, consulte [asignación de tipos de datos de DB2 y SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md).  
  
-   Si no tiene que realizar ninguna de estas tareas, puede convertir las definiciones de objetos de base de datos DB2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en definiciones de objeto. Para obtener más información, vea [convertir esquemas DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md).  
  
## <a name="see-also"></a>Consulte también  
[Migrar bases de datos DB2 a SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  

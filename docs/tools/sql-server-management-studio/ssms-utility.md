---
title: "Ssms (Utilidad) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQL Server Management Studio [SQL Server], abrir"
  - "utilidades del símbolo del sistema [SQL Server], sqlwb"
  - "sqlwb, utilidad"
  - "Management Studio, línea de comandos"
  - "abrir SQL Server Management Studio"
ms.assetid: aafda520-9e2a-4e1e-b936-1b165f1684e8
caps.latest.revision: 50
author: "stevestein"
ms.author: "sstein"
manager: "jhubbard"
caps.handback.revision: 50
---
# Ssms (Utilidad)
  La utilidad **Ssms**abre [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Si se especifica, **Ssms** también establece una conexión con un servidor y abre consultas, scripts, archivos, proyectos y soluciones.  
  
 Puede especificar archivos que contienen consultas, proyectos o soluciones. Los archivos que contienen consultas se conectan automáticamente con un servidor si se proporciona información de conexión y el tipo de archivo está asociado con ese tipo de servidor. Por ejemplo, los archivos .sql abrirán una ventana del Editor de consultas de SQL en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], y los archivos .mdx abrirán una ventana del Editor de consultas MDX en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Las**Soluciones y proyectos de SQL Server** se abrirán en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
> [!NOTE]  
>  La utilidad **Ssms** no ejecuta consultas. Para ejecutar consultas desde la línea de comandos, utilice la utilidad **sqlcmd** .  
  
## Sintaxis  
  
```  
  
Ssms  
    [scriptfile] [projectfile] [solutionfile]  
    [-S servername] [-d databasename] [-U username] [-P password]   
    [-E] [-nosplash] [-log [filename]?] [-?]  
```  
  
## Argumentos  
 *scriptfile*  
 Especifica uno o más archivos de script para abrirlos. El parámetro debe contener la ruta completa a los archivos.  
  
 *projectfile*  
 Especifica un proyecto de script para abrirlo. El parámetro debe contener la ruta completa al archivo del proyecto de script.  
  
 *solutionfile*  
 Especifica una solución para abrirla. El parámetro debe contener la ruta completa al archivo de solución.  
  
 [**-S** *servername*]  
 Nombre del servidor  
  
 [**-d** *databasename*]  
 Nombre de la base de datos  
  
 [**-U** *username*]  
 Nombre de usuario cuando se conecta con la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 [**-P** *password*]  
 Contraseña cuando se conecta con la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 [**-E**]  
 Conectar con la autenticación de Windows.  
  
 [**-nosplash**]  
 Impide que [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] muestre el gráfico de la pantalla de presentación mientras se abre. Utilice esta opción cuando se conecte con un equipo que ejecute [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] mediante Terminal Services en una conexión con ancho de banda limitado. Este argumento no distingue entre mayúsculas y minúsculas y puede aparecer antes o después de otros argumentos.  
  
 [**-log***[filename]?*]  
 Registra la actividad de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] en el archivo especificado para la solución de problemas  
  
 [**-?**]  
 Muestra la ayuda de la línea de comandos.  
  
## Comentarios  
 Todos los modificadores son opcionales y están separados por un espacio, excepto los archivos, que están separados por comas. Si no especifica modificadores, **Ssms** abre [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] según se especifica en la configuración de **Opciones** del menú **Herramientas** . Por ejemplo, si en la página **Entorno/General**, la opción **Al iniciar** especifica **Abrir nueva ventana de consulta**, **Ssms** se abrirá con un Editor de consultas en blanco.  
  
 El modificador **-log** debe aparecer al final de la línea de comandos, después de todos los demás modificadores. El argumento de nombre de archivo es opcional. Si se especifica un nombre de archivo y el archivo no existe, este se crea. Si no es posible crear el archivo, por ejemplo, debido a un acceso de escritura insuficiente, el registro se escribe en la ubicación APPDATA no localizada (ver más abajo). Si no se especifica el argumento de nombre de archivo, se escriben dos archivos en la carpeta de datos de la aplicación no localizada del usuario actual. La carpeta de datos de la aplicación no localizada para SQL Server se puede obtener de la variable de entorno APPDATA. Por ejemplo, para SQL Server 2012, la carpeta es \<unidadDelSistema>:\Users\\<nombreDeUsuario\>\AppData\Roaming\Microsoft\AppEnv\10.0\\. De forma predeterminada, los dos archivos se denominan ActivityLog.xml y ActivityLog.xsl. El primero contiene los datos del registro de actividad y el segundo es una hoja de estilos XML que permite visualizar correctamente el archivo XML. Haga lo siguiente para ver el archivo de registro en el visor XML predeterminado, como Internet Explorer: haga clic en Inicio y, después, en Ejecutar...; luego, escriba “\<unidadDelSistema>:\Users\\<nombreDeUsuario\>\AppData\Roaming\Microsoft\AppEnv\10.0\ActivityLog.xml” en el campo proporcionado y, por último, pulse Entrar.  
  
 Los archivos que contienen consultas solicitarán la conexión con un servidor si se proporciona información de conexión y el tipo de archivo está asociado con ese tipo de servidor. Por ejemplo, los archivos .sql abrirán una ventana del Editor de consultas de SQL en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], y los archivos .mdx abrirán una ventana del Editor de consultas MDX en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Las**Soluciones y proyectos de SQL Server** se abrirán en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 La siguiente tabla asigna tipos de servidores a extensiones de archivos.  
  
|Tipo de servidor|Extensión|  
|-----------------|---------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|.sql|  
|SQL Server Analysis Services|.mdx<br /><br /> .xmla|  
  
## Ejemplos  
 El siguiente script abre [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] desde un símbolo del sistema con la configuración predeterminada:  
  
```  
Ssms  
  
```  
  
 El siguiente script abre [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] desde un símbolo del sistema, con autenticación de Windows, con el Editor de código establecido en el servidor `ACCTG and the database AdventureWorks2012,` sin mostrar la pantalla de presentación:  
  
```  
Ssms -E -S ACCTG -d AdventureWorks2012 -nosplash  
  
```  
  
 El siguiente script abre [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] desde un símbolo del sistema y abre el script de MonthEndQuery:  
  
```  
Ssms "C:\Documents and Settings\username\My Documents\SQL Server Management Studio Projects\FinanceScripts\FinanceScripts\MonthEndQuery.sql"  
  
```  
  
 El siguiente script abre [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] desde un símbolo del sistema y abre el proyecto NewReportsProject en el equipo denominado `developer`:  
  
```  
Ssms "\\developer\fin\ReportProj\ReportProj\NewReportProj.ssmssqlproj"  
  
```  
  
 El siguiente script abre [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] desde un símbolo del sistema y abre la solución MonthlyReports:  
  
```  
Ssms "C:\solutionsfolder\ReportProj\MonthlyReports.ssmssln"  
  
```  
  
## Vea también  
 [Usar SQL Server Management Studio](../../ssms/use-sql-server-management-studio.md)  
  
  
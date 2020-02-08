---
title: Validar un paquete de DAC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- data-tier application [SQL Server], validate
- data-tier application [SQL Server], compare
- validate DAC
- compare DACs
- data-tier application [SQL Server], view
- view DAC
ms.assetid: 726ffcc2-9221-424a-8477-99e3f85f03bd
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7df5bb3b2ef677e597d12dad8b8d92ddbb22fcba
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "72908246"
---
# <a name="validate-a-dac-package"></a>Validar un paquete de DAC
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Es aconsejable revisar el contenido de un paquete DAC antes de implementarlo en producción y validar las acciones de actualización antes de actualizar una DAC existente. Esto es especialmente aconsejable al implementar paquetes que no se desarrollaron en su organización.  
  
1.  **Antes de empezar:**  [Requisitos previos](#Prerequisites)  
  
2.  **Para actualizar una DAC mediante:**  [Ver el contenido de una DAC](#ViewDACContents), [Ver los cambios de la base de datos](#ViewDBChanges), [Ver las acciones de actualización](#ViewUpgradeActions), [Comparar las DAC](#CompareDACs)  

##  <a name="Prerequisites"></a> Requisitos previos  
 Se recomienda no implementar un paquete DAC desde orígenes desconocidos o que no sean de confianza. Es posible que estas DAC contengan código malintencionado que podría ejecutar código [!INCLUDE[tsql](../../includes/tsql-md.md)] no deseado o provocar errores al modificar el esquema. Antes de usar una DAC de un origen desconocido o que no sea de confianza, impleméntela en una instancia de prueba aislada de [!INCLUDE[ssDE](../../includes/ssde-md.md)], ejecute [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) en la base de datos y examine también el código en la base de datos, como los procedimientos almacenados u otro código definido por el usuario.  
  
##  <a name="ViewDACContents"></a> Ver el contenido de una DAC  
 Hay dos mecanismos para ver el contenido de un paquete de aplicación de capa de datos (DAC). Puede importar el paquete DAC a un proyecto DAC en SQL Server Developer Tools. Puede desempaquetar el contenido del paquete en una carpeta.  
  
 **Ver una DAC en SQL Server Developer Tools**  
  
1.  Abra el menú **Archivo**, seleccione **Nuevo** y, después, **Proyecto...** .  
  
2.  Seleccione la plantilla de proyecto de **SQL Server** y especifique los valores de **Nombre**, **Ubicación**y **Nombre de solución**.  
  
3.  En el **Explorador de soluciones**, haga clic con el botón derecho en el nodo y seleccione **Propiedades...** .  
  
4.  En la pestaña **Configuración de proyecto** , en la sección **Tipos de salida** , active la casilla **Aplicación de capa de datos (archivo .dacpac)** y, después, cierre el cuadro de diálogo de propiedades.  
  
5.  En el **Explorador de soluciones**, haga clic con el botón derecho en el nodo de proyecto y seleccione **Importar aplicación de capa de datos...** .  
  
6.  Use el **Explorador de soluciones** para abrir todos los archivos de la DAC, como la directiva de selección de servidor y los scripts previos y posteriores a la implementación.  
  
7.  Use la **Vista de esquema** para revisar todos los objetos en el esquema, especialmente el código en objetos, como funciones o procedimientos almacenados.  
  
 **Ver una DAC en una carpeta**  
  
-   Desempaquete el paquete DAC en una carpeta según las instrucciones de [Unpack a DAC Package](../../relational-databases/data-tier-applications/unpack-a-dac-package.md).  
  
-   Para ver el contenido de los scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] , ábralos en el editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
-   Vea el contenido de los archivos de texto en herramientas como Bloc de notas.  
  
##  <a name="ViewDBChanges"></a> Ver los cambios de la base de datos  
 Después de que la versión actual de una DAC se haya implementado en producción, los cambios que se pueden haber realizado directamente en la base de datos asociada pueden estar en conflicto con el esquema definido en una nueva versión de la DAC. Antes de actualizar a una nueva versión de la DAC, compruebe si estos cambios se han realizado en la base de datos.  
  
 **Ver los cambios de la base de datos mediante un asistente**  
  
1.  Ejecute el asistente **Actualizar aplicación de capa de datos** , y especifique la DAC implementada actualmente y el paquete DAC que contiene la nueva versión de la DAC.  
  
2.  En la página **Detectar cambio** , revise el informe de los cambios que se han realizado en la base de datos.  
  
3.  Seleccione **Cancelar** si no desea continuar con la actualización.  
  
4.  Para obtener más información sobre cómo usar el asistente, vea [Actualizar una aplicación de capa de datos](../../relational-databases/data-tier-applications/upgrade-a-data-tier-application.md).  
  
 **Ver los cambios de las bases de datos mediante PowerShell**  
  
1.  Cree un objeto SMO Server y establézcalo en la instancia que contiene la DAC que se va a ver.  
  
2.  Abra un objeto **ServerConnection** y conéctese a la misma instancia.  
  
3.  Especifique el nombre de DAC en una variable.  
  
4.  Use el método **GetDatabaseChanges()** para recuperar un objeto **ChangeResults** y canalícelo a un archivo de texto para generar un informe simple de objetos nuevos, eliminados y cambiados.  
  
### <a name="view-database-changes-example-powershell"></a>Ver el ejemplo de cambios de base de datos (PowerShell)  
 **Ver el ejemplo de cambios de base de datos (PowerShell)**  
  
 El ejemplo siguiente informa de los cambios de base de datos que se hayan realizado en una DAC implementada con el nombre MyApplication.  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Specify the DAC instance name.  
$dacName  = "MyApplication"  
  
## Generate the change list and save to file.  
$dacChanges = $dacstore.GetDatabaseChanges($dacName) | Out-File -Filepath C:\DACScripts\MyApplicationChanges.txt  
```  
  
##  <a name="ViewUpgradeActions"></a> Ver las acciones de actualización  
 Antes de usar una versión nueva de un paquete DAC para actualizar una DAC que se implementó a partir de un paquete DAC anterior, puede generar un informe que contenga las instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] que se ejecutarán durante la actualización y, después, revisar las instrucciones.  
  
 **Acciones de actualización de informe mediante un asistente**  
  
1.  Ejecute el asistente **Actualizar aplicación de capa de datos** , y especifique la DAC implementada actualmente y el paquete DAC que contiene la nueva versión de la DAC.  
  
2.  En la página **Resumen** , revise el informe de las acciones de actualización.  
  
3.  Seleccione **Cancelar** si no desea continuar con la actualización.  
  
4.  Para obtener más información sobre cómo usar el asistente, vea [Actualizar una aplicación de capa de datos](../../relational-databases/data-tier-applications/upgrade-a-data-tier-application.md).  
  
 **Acciones de actualización de informe mediante PowerShell**  
  
1.  Cree un objeto SMO Server y establézcalo en la instancia que contiene la DAC implementada.  
  
2.  Abra un objeto **ServerConnection** y conéctese a la misma instancia.  
  
3.  Use **System.IO.File** para cargar el archivo de paquete DAC.  
  
4.  Especifique el nombre de DAC en una variable.  
  
5.  Use el método **GetIncrementalUpgradeScript()** para obtener una lista de las instrucciones Transact-SQL que ejecutaría una actualización y canalice dicha lista a un archivo de texto.  
  
6.  Cierra la secuencia de archivos usada para leer el archivo de paquete DAC.  
  
### <a name="view-upgrade-actions-example-powershell"></a>Ver el ejemplo de acciones de actualización (PowerShell)  
 **Ver el ejemplo de acciones de actualización (PowerShell)**  
  
 En el siguiente ejemplo, se proporcionan instrucciones Transact-SQL que se ejecutan para actualizar una DAC denominada MyApplication en el esquema definido en un archivo MyApplication2017.dacpac.  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Load the DAC package file.  
$dacpacPath = "C:\MyDACs\MyApplication2017.dacpac"  
$fileStream = [System.IO.File]::Open($dacpacPath,[System.IO.FileMode]::OpenOrCreate)  
$dacType = [Microsoft.SqlServer.Management.Dac.DacType]::Load($fileStream)  
  
## Specify the DAC instance name.  
$dacName  = "MyApplication"  
  
## Generate the upgrade script and save to file.  
$dacstore.GetIncrementalUpgradeScript($dacName, $dacType) | Out-File -Filepath C:\DACScripts\MyApplicationUpgrade.sql  
  
## Close the filestream to the new DAC package.  
$fileStream.Close()  
```  
  
##  <a name="CompareDACs"></a> Compare DACs  
 Antes de actualizar una DAC, es aconsejable revisar las diferencias en la base de datos y los objetos en el nivel de instancia entre la DAC actual y la nueva. Si no tiene una copia del paquete de la DAC actual, puede extraer un paquete de la base de datos actual.  
  
 Si importa ambos paquetes DAC en proyectos DAC en SQL Server Developer Tools, puede usar la herramienta de comparación de esquemas para analizar las diferencias entre las dos DAC.  
  
 O bien, desempaquete las DAC en carpetas independientes. A continuación, puede usar una herramienta de diferenciación, como la utilidad WinDiff, para analizar las diferencias.  
  
## <a name="see-also"></a>Consulte también  
 [Aplicaciones de capa de datos](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Implementar una aplicación de capa de datos](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)   
 [Actualizar una aplicación de capa de datos](../../relational-databases/data-tier-applications/upgrade-a-data-tier-application.md)  
  
  

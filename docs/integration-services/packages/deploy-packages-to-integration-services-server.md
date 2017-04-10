---
title: "Implementaci&#243;n de paquetes en el servidor de Integration Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c26ce7f4-7b34-4c9a-8649-ba767d30c827
caps.latest.revision: 10
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# Implementaci&#243;n de paquetes en el servidor de Integration Services
  La característica Implementación incremental de paquetes presentada en  [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] le permite implementar uno o varios paquetes en un proyecto nuevo o existente sin implementar todo el proyecto.  
  
##  <a name="DeployWizard"></a> Implementación de paquetes mediante el Asistente para implementación de Integration Services  
  
1.  En el símbolo del sistema, ejecute **isdeploymentwizard.exe** de **%Archivos de programa%\Microsoft SQL Server\130\DTS\Binn**. En equipos de 64 bits, también hay una versión de 32 bits de la herramienta en **%Archivos de programa (x86)%\Microsoft SQL Server\130\DTS\Binn**.  
  
2.  En la página **Seleccionar origen** , cambie a **Modelo de implementación de paquetes**. A continuación, seleccione la carpeta que contiene los paquetes de origen y configúrelos.  
  
3.  Finalice el asistente. Siga los pasos restantes descritos en [Package Deployment Model](../../integration-services/packages/integration-services-deployment-wizard.md#PackageModel).  
  
##  <a name="SSMS"></a> Implementación de paquetes mediante SQL Server Management Studio  
  
1.  En SQL Server Management Studio, expanda el nodo **Catálogos de Integration Services** > **SSISDB** en el Explorador de objetos.  
  
2.  Haga clic con el botón derecho en la carpeta **Proyectos** y luego en **Implementar proyectos**.  
  
3.  Si ve la página **Introducción** , haga clic en **Siguiente** para continuar.  
  
4.  En la página **Seleccionar origen** , cambie a **Modelo de implementación de paquetes**. A continuación, seleccione la carpeta que contiene los paquetes de origen y configúrelos.  
  
5.  Finalice el asistente. Siga los pasos restantes descritos en [Package Deployment Model](../../integration-services/packages/integration-services-deployment-wizard.md#PackageModel).  
  
##  <a name="SSDT"></a> Implementación de paquetes mediante SQL Server Data Tools (Visual Studio)  
  
1.  En Visual Studio, con un proyecto de Integration Services abierto, seleccione el paquete o paquetes que desea implementar.  
  
2.  Haga clic con el botón derecho y seleccione **Implementar paquete**. Se abre el Asistente para implementación con los paquetes seleccionados configurados como los paquetes de origen.  
  
3.  Finalice el asistente. Siga los pasos restantes descritos en [Package Deployment Model](../../integration-services/packages/integration-services-deployment-wizard.md#PackageModel).  
  
##  <a name="StoredProcedure"></a> Implementación de paquetes mediante el procedimiento almacenado deploy_packages  
 Puede usar el procedimiento almacenado **[catalog].[deploy_packages]** para implementar uno o más paquetes SSIS en el catálogo de SSIS. En el ejemplo de código siguiente se muestra el uso de este procedimiento almacenado para implementar paquetes en un servidor de SSIS. Para obtener más información, vea [catalog.deploy_packages](../../integration-services/system-stored-procedures/catalog-deploy-packages.md).  
  
```  
  
private static void Main(string[] args)  
{  
    // Connection string to SSISDB  
    var connectionString = "Data Source=.;Initial Catalog=SSISDB;Integrated Security=True;MultipleActiveResultSets=false";  
  
    using (var sqlConnection = new SqlConnection(connectionString))  
    {  
        sqlConnection.Open();  
  
        var sqlCommand = new SqlCommand  
        {  
            Connection = sqlConnection,  
            CommandType = CommandType.StoredProcedure,  
            CommandText = "[catalog].[deploy_packages]"  
        };  
  
        var packageData = Encoding.UTF8.GetBytes(File.ReadAllText(@"C:\Test\Package.dtsx"));  
  
        // DataTable: name is the package name without extension and package_data is byte array of package.  
        var packageTable = new DataTable();  
        packageTable.Columns.Add("name", typeof(string));  
        packageTable.Columns.Add("package_data", typeof(byte[]));  
        packageTable.Rows.Add("Package", packageData);  
  
        // Set the destination project and folder which is named Folder and Project.  
        sqlCommand.Parameters.Add(new SqlParameter("@folder_name", SqlDbType.NVarChar, ParameterDirection.Input, "Folder", -1));  
        sqlCommand.Parameters.Add(new SqlParameter("@project_name", SqlDbType.NVarChar, ParameterDirection.Input, "Project", -1));  
        sqlCommand.Parameters.Add(new SqlParameter("@packages_table", SqlDbType.Structured, ParameterDirection.Input, packageTable, -1));  
  
        var result = sqlCommand.Parameters.Add("RetVal", SqlDbType.Int);  
        result.Direction = ParameterDirection.ReturnValue;  
  
        sqlCommand.ExecuteNonQuery();  
    }  
}  
  
```  
  
##  <a name="MOMApi"></a> Implementación de paquetes mediante la API del modelo de objetos de administración  
 En el ejemplo de código siguiente se muestra el uso de la API del modelo de objetos de administración para implementar paquetes en un servidor.  
  
```  
  
static void Main()  
 {  
     // Before deploying packages, make sure the destination project exists in SSISDB.  
     var connectionString = "Data Source=.;Integrated Security=True;MultipleActiveResultSets=false";  
     var catalogName = "SSISDB";  
     var folderName = "Folder";  
     var projectName = "Project";  
  
     // Get the folder instance.  
     var sqlConnection = new SqlConnection(connectionString);  
     var store = new Microsoft.SqlServer.Management.IntegrationServices.IntegrationServices(sqlConnection);  
     var folder = store.Catalogs[catalogName].Folders[folderName];  
  
     // Key is package name without extension and value is package binaries.  
     var packageDict = new Dictionary<string, string>();  
  
     var packageData = File.ReadAllText(@"C:\Folder\Package.dtsx");  
     packageDict.Add("Package", packageData);  
  
     // Deploy package to the destination project.  
     folder.DeployPackages(projectName, packageDict);  
 }  
  
```  
  
  
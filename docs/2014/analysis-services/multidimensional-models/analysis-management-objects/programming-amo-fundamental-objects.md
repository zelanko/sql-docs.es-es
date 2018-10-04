---
title: Programar objetos fundamentales de AMO | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- server objects [AMO]
- programming [AMO]
- AMO, database objects
- AMO, server objects
- Analysis Management Objects, server objects
- database objects [AMO]
- Analysis Management Objects, database objects
ms.assetid: 3f1ab656-f3bc-432d-8b6d-cdf204e5be10
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cc100d99d3e125c22c04aac8cf092646f2b0cfa1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48168995"
---
# <a name="programming-amo-fundamental-objects"></a>Programar objetos fundamentales de AMO
  Los objetos fundamentales son generalmente objetos simples y sencillos. Estos objetos se crean normalmente con instancias y después, cuando ya no se necesitan, el usuario se desconecta de ellos. Las clases fundamentales incluyen los objetos siguientes: <xref:Microsoft.AnalysisServices.Server>, <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.DataSource>y <xref:Microsoft.AnalysisServices.DataSourceView>. El único objeto complejo en los objetos fundamentales de AMO es <xref:Microsoft.AnalysisServices.DataSourceView>, que requiere detalles para generar el modelo abstracto que representa la vista del origen de datos.  
  
 Normalmente, se requiere que los objetos <xref:Microsoft.AnalysisServices.Server> y <xref:Microsoft.AnalysisServices.Database> usen los objetos contenidos como objetos OLAP u objetos de minería de datos.  
  
 Este tema contiene las siguientes secciones:  
  
-   [Objetos de servidor](#ServerObjects)  
  
-   [Objetos de excepción AMOException](#AMO)  
  
-   [Objetos de base de datos](#DatabaseObjects)  
  
-   [Objetos DataSource](#DataSource)  
  
-   [Objetos DataSourceView](#DSV)  
  
##  <a name="ServerObjects"></a> Objetos de servidor  
 Para usar un <xref:Microsoft.AnalysisServices.Server> objeto requiere los pasos siguientes: conectarse al servidor, comprobar si el <xref:Microsoft.AnalysisServices.Server> de objetos está conectado al servidor y, si es así, desconectar el <xref:Microsoft.AnalysisServices.Server> desde el servidor.  
  
### <a name="connecting-to-the-server-object"></a>Conectar al objeto Server  
 Para conectarse al servidor de debe tener la cadena de conexión correcta.  
  
 En el ejemplo de código siguiente se devuelve un objeto <xref:Microsoft.AnalysisServices.Server> si la conexión es correcta o se devuelve `null` si se produce un error. Los errores durante el proceso de conexión se administran en una construcción de try/catch. Los errores AMO se detectan mediante la clase de excepción <xref:Microsoft.AnalysisServices.AmoException>. En este ejemplo, el error se muestra al usuario en un cuadro de mensaje.  
  
```  
static Server ServerConnect( String strStringConnection)  
{  
    string methodCaption = "ServerConnect method";  
    Server svr = new Server();  
    try  
    {  
        svr.Connect(strStringConnection);  
    }  
    #region ErrorHandling  
    catch (AmoException e)  
    {  
        MessageBox.Show( "AMO exception " + e.ToString());  
        svr = null;  
    }  
    catch (Exception e)  
    {  
        MessageBox.Show("General exception " + e.ToString());  
        svr = null;  
    }  
    #endregion  
  
    return svr;  
}  
```  
  
 La estructura de la cadena de conexión es:  
  
 "**Origen de datos =**\<nombre del servidor >".  
  
 Para obtener más información acerca de las cadenas de conexión, vea <xref:Microsoft.SqlServer.Management.Common.OlapConnectionInfo.ConnectionString%2A>.  
  
### <a name="validating-the-connection"></a>Validar la conexión  
 Antes de programar los objetos <xref:Microsoft.AnalysisServices.Server>, debería comprobar si aún está conectado al servidor. En el ejemplo de código siguiente se muestra cómo hacerlo. En el ejemplo se supone que `svr` es un objeto <xref:Microsoft.AnalysisServices.Server> que existe en su código.  
  
```  
if ( (svr != null) && ( svr.Connected))  
{  
    // Do what it is needed if connection is good  
}  
```  
  
### <a name="disconnecting-from-the-server"></a>Desconectar del servidor  
 En cuanto termine, puede desconectarse del servidor mediante el método Disconnect. En el ejemplo de código siguiente se muestra cómo hacerlo. En el ejemplo se supone que `svr` es un objeto <xref:Microsoft.AnalysisServices.Server> que existe en su código.  
  
```  
if ( (svr != null) && ( svr.Connected))  
{  
    svr.Disconnect()  
}  
```  
  
###  <a name="AMO"></a> Objetos de excepción AmoException  
 AMO producirá excepciones en los diferentes problemas encontrados. Para obtener una explicación detallada de excepciones, vea [AMO otras clases y métodos](amo-other-classes-and-methods.md). En el código de ejemplo siguiente se muestra la manera correcta de capturar excepciones en AMO:  
  
```  
try  
{  
   //... some AMO code in here  
}  
  
catch (  OutOfSynchException e)  
{  
   // error handling code for OutOfSynchException   
}  
  
catch (  OperationException e)  
{  
   // error handling code for OperationException   
}   
  
catch (  ResponseFormatException e)  
  
{  
   // error handling code for ResponseFormatException   
}   
  
catch (  ConnectionException e)  
  
{  
   // error handling code for ConnectionException   
}  
  
catch (  AMOException e)  
  
{  
   //... here is the place where you end if it is an AMO exception, but none of the previous exceptions  
   // if you start with AMOException in the first catch you will never see any one of the previous exceptions  
}  
```  
  
##  <a name="DatabaseObjects"></a> Objetos de base de datos  
 Trabajar con un objeto <xref:Microsoft.AnalysisServices.Database> es muy simple y sencillo. Obtendrá una base de datos existente de la colección de bases de datos del objeto <xref:Microsoft.AnalysisServices.Server>.  
  
### <a name="creating-dropping-and-finding-a-database"></a>Crear, quitar y buscar una base de datos  
 En el ejemplo de código siguiente se muestra cómo crear una base de datos mediante un nombre de base de datos. Antes de crear la base de datos, realice una consulta a <xref:Microsoft.AnalysisServices.DatabaseCollection> del servidor para comprobar si existe esa base de datos. Si la base de datos existe, se quita y posteriormente se crea; si la base de datos no existe, se crea. Si la base de datos se va a quitar, primero se adquiere esa base de datos de la colección de bases de datos.  
  
```  
static Database CreateDatabase(Server svr, String DatabaseName)  
{  
    Database db = null;  
    if ( (svr != null) && ( svr.Connected))  
    {  
        // Drop the database if it already exists  
        db = svr.Databases.FindByName(DatabaseName);  
        if (db != null)  
        {  
            db.Drop();  
        }  
  
        // Create the database  
        db = svr.Databases.Add(DatabaseName);  
        db.Update();  
    }  
  
    return db;  
}  
```  
  
 Para determinar si una base de datos existe en la colección de bases de datos, se usa el método FindByName. Si la base de datos existe, el método devuelve el objeto de la base de datos encontrado, si no devuelve un objeto null.  
  
 Tan pronto como se agregue el objeto <xref:Microsoft.AnalysisServices.Database> a la colección de bases de datos, el servidor debe actualizarse mediante su propio método Update. Un error en la actualización del servidor provocará que el objeto <xref:Microsoft.AnalysisServices.Database> no se cree en el servidor.  
  
### <a name="processing-a-database"></a>Procesar una base de datos  
 Procesar una base de datos, con todos los objetos secundarios, es muy simple porque el objeto <xref:Microsoft.AnalysisServices.Database> incluye un método Process.  
  
 El método Process puede incluir parámetros, pero no son necesarios. Si no se especifica ningún parámetro, todos los objetos secundarios se procesarán con su propia opción `ProcessDefault`. Para obtener más información acerca de las opciones de procesamiento, vea <xref:Microsoft.AnalysisServices.Database>.  
  
1.  En el código de ejemplo siguiente se procesa una base de datos mediante su propio valor predeterminado.  
  
```  
static Database ProcessDatabase(Database db, ProcessType pt)  
{  
    db.Process( pt);  
    return db;  
}  
```  
  
##  <a name="DataSource"></a> Objetos DataSource  
 Un objeto <xref:Microsoft.AnalysisServices.DataSource> es el vínculo entre [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] y la base de datos donde residen los datos. El objeto <xref:Microsoft.AnalysisServices.DataSourceView> define el esquema que representa el modelo subyacente para [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Un objeto <xref:Microsoft.AnalysisServices.DataSource> se puede considerar como una cadena de conexión a la base de datos donde residen los datos.  
  
 En el código de ejemplo siguiente se muestra cómo se crea un objeto <xref:Microsoft.AnalysisServices.DataSource>. En el ejemplo se comprueba que el servidor todavía existe, el objeto <xref:Microsoft.AnalysisServices.Server> está conectado y la base de datos existe. Si el objeto <xref:Microsoft.AnalysisServices.DataSource> existe, se quita y se vuelve a crear. El objeto <xref:Microsoft.AnalysisServices.DataSource> se crea con el mismo nombre e identificador interno. En este ejemplo, no se realiza ninguna comprobación en la cadena de conexión para indicarlo.  
  
```  
static string CreateDataSource(Database db, string strDataSourceName, string strConnectionString)  
{  
        Server svr = db.Parent;  
        DataSource ds = db.DataSources.FindByName(strDataSourceName);  
        if (ds != null)  
            ds.Drop();  
        // Create the data source  
        ds = db.DataSources.Add(strDataSourceName, strDataSourceName);  
        ds.ConnectionString = strConnectionString;  
  
        // Send the data source definition to the server.  
        ds.Update();  
  
        return ds.Name;  
}  
```  
  
##  <a name="DSV"></a> Objetos DataSourceView  
 El objeto <xref:Microsoft.AnalysisServices.DataSourceView> es el responsable de almacenar el modelo del esquema para [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Para que el objeto <xref:Microsoft.AnalysisServices.DataSourceView> almacene el esquema, primero se debe construir el esquema. Los esquemas se construyen sobre los objetos DataSet, del espacio de nombres System.Data.  
  
 En el código de ejemplo siguiente se creará parte del esquema que se incluye en el proyecto de ejemplo de Analysis Services basado en AdventureWorks. En el ejemplo se crean definiciones de esquema para las tablas, columnas calculadas, relaciones y relaciones compuestas. Los esquemas son conjuntos de datos permanentes.  
  
 En el código de ejemplo se realizan las tareas siguientes:  
  
1.  Crear un objeto <xref:Microsoft.AnalysisServices.DataSourceView>.  
  
     Compruebe primero si existe el objeto <xref:Microsoft.AnalysisServices.DataSource>; si es `true`, quite y cree <xref:Microsoft.AnalysisServices.DataSource>. Si no existe <xref:Microsoft.AnalysisServices.DataSource>, créelo.  
  
2.  Abrir una conexión a la base de datos mediante la cadena de conexión <xref:Microsoft.AnalysisServices.DataSource>.  
  
3.  Crear el esquema.  
  
     El esquema consta de:  
  
    -   Una definición de tabla, método `AddTable()`.  
  
    -   Un conjunto opcional de columnas calculadas, método `AddComputedColumn()`.  
  
    -   Un conjunto opcional de relaciones, `AddRelation`.  
  
    -   Un conjunto opcional de relaciones compuestas, `AddCompositeRelations`.  
  
4.  Actualizar el servidor.  
  
> [!NOTE]  
>  El código de ejemplo siguiente se recorta con fines de legibilidad; el código completo se incluye al final de este tema.  
  
> [!NOTE]  
>  Los métodos siguientes forman parte del código de ejemplo: `AddTable`, `AddComputedColumn`, `AddRelation` y `AddCompositeRelation`.  
  
> [!NOTE]  
>  La cláusula `'WHERE 1=0'` es para evitar que la consulta devuelva filas al objeto `DataSet`.  
  
```  
        static DataSourceView CreateDataSourceView(Database db, string strDataSourceName)  
        {  
            // Create the data source view  
            DataSourceView dsv = db.DataSourceViews.FindByName(strDataSourceName);  
            if ( dsv != null)  
               dsv.Drop();  
            dsv = db.DataSourceViews.Add(strDataSourceName);  
            dsv.DataSourceID = strDataSourceName;  
            dsv.Schema = new DataSet();  
            dsv.Schema.Locale = CultureInfo.CurrentCulture;  
  
            // Open a connection to the data source  
            OleDbConnection connection  
                = new OleDbConnection(dsv.DataSource.ConnectionString);  
            connection.Open();  
  
            #region Create tables  
  
            // Add the DimTime table  
            AddTable(dsv, connection, "DimTime");  
            AddComputedColumn(dsv, connection, "DimTime", "SimpleDate", "DATENAME(mm, FullDateAlternateKey) + ' ' + DATENAME(dd, FullDateAlternateKey) + ',' + ' ' + DATENAME(yy, FullDateAlternateKey)");  
  
            // Add the DimProductCategory table  
            AddTable(dsv, connection, "DimProductCategory");  
  
            // Add the DimProductSubcategory table  
            AddTable(dsv, connection, "DimProductSubcategory");  
            AddRelation(dsv, "DimProductSubcategory", "ProductCategoryKey", "DimProductCategory", "ProductCategoryKey");  
  
            // Add the FactInternetSales table  
            AddTable(dsv, connection, "FactInternetSales");  
"DimTime", "TimeKey");  
            AddRelation(dsv, "FactInternetSales", "ShipDateKey", "DimTime", "TimeKey");  
            AddRelation(dsv, "FactInternetSales", "DueDateKey", "DimTime", "TimeKey");  
  
            // Add the FactInternetSalesReason table  
            AddTable(dsv, connection, "FactInternetSalesReason");  
            AddCompositeRelation(dsv, "FactInternetSalesReason", "FactInternetSales", "SalesOrderNumber", "SalesOrderLineNumber");  
            dsv.Update();  
  
            #endregion  
  
            // Send the data source view definition to the server  
            dsv.Update();  
  
            return dsv;  
        }  
  
        static void AddTable(DataSourceView dsv, OleDbConnection connection, String tableName)  
        {  
            string strSelectText = "SELECT * FROM [dbo].[" + tableName + "] WHERE 1=0";  
            OleDbDataAdapter adapter = new OleDbDataAdapter(strSelectText, connection);  
            DataTable[] dataTables = adapter.FillSchema(dsv.Schema,  
                SchemaType.Mapped, tableName);  
            DataTable dataTable = dataTables[0];  
  
            dataTable.ExtendedProperties.Add("TableType", "Table");  
            dataTable.ExtendedProperties.Add("DbSchemaName", "dbo");  
            dataTable.ExtendedProperties.Add("DbTableName", tableName);  
            dataTable.ExtendedProperties.Add("FriendlyName", tableName);  
  
            dataTable = null;  
            dataTables = null;  
            adapter = null;  
        }  
  
        static void AddComputedColumn(DataSourceView dsv, OleDbConnection connection, String tableName, String computedColumnName, String expression)  
        {  
            DataSet tmpDataSet = new DataSet();  
            tmpDataSet.Locale = CultureInfo.CurrentCulture;  
            OleDbDataAdapter adapter = new OleDbDataAdapter("SELECT ("  
                + expression + ") AS [" + computedColumnName + "] FROM [dbo].["  
                + tableName + "] WHERE 1=0", connection);  
            DataTable[] dataTables = adapter.FillSchema(tmpDataSet,  
                SchemaType.Mapped, tableName);  
            DataTable dataTable = dataTables[0];  
            DataColumn dataColumn = dataTable.Columns[computedColumnName];  
  
            dataTable.Constraints.Clear();  
            dataTable.Columns.Remove(dataColumn);  
  
            dataColumn.ExtendedProperties.Add("DbColumnName", computedColumnName);  
            dataColumn.ExtendedProperties.Add("ComputedColumnExpression",  
                expression);  
            dataColumn.ExtendedProperties.Add("IsLogical", "True");  
  
            dsv.Schema.Tables[tableName].Columns.Add(dataColumn);  
  
            dataColumn = null;  
            dataTable = null;  
            dataTables = null;  
            adapter = null;  
            tmpDataSet = null;  
        }  
  
        static void AddRelation(DataSourceView dsv, String fkTableName, String fkColumnName, String pkTableName, String pkColumnName)  
        {  
            DataColumn fkColumn  
                = dsv.Schema.Tables[fkTableName].Columns[fkColumnName];  
            DataColumn pkColumn  
                = dsv.Schema.Tables[pkTableName].Columns[pkColumnName];  
            dsv.Schema.Relations.Add("FK_" + fkTableName + "_"  
                + fkColumnName, pkColumn, fkColumn, true);  
        }  
  
        static void AddCompositeRelation(DataSourceView dsv, String fkTableName, String pkTableName, String columnName1, String columnName2)  
        {  
            DataColumn[] fkColumns = new DataColumn[2];  
            fkColumns[0] = dsv.Schema.Tables[fkTableName].Columns[columnName1];  
            fkColumns[1] = dsv.Schema.Tables[fkTableName].Columns[columnName2];  
  
            DataColumn[] pkColumns = new DataColumn[2];  
            pkColumns[0] = dsv.Schema.Tables[pkTableName].Columns[columnName1];  
            pkColumns[1] = dsv.Schema.Tables[pkTableName].Columns[columnName2];  
  
            dsv.Schema.Relations.Add("FK_" + fkTableName + "_" + columnName1  
                + "_" + columnName2, pkColumns, fkColumns, true);  
        }  
  
```  
  
 En el código de ejemplo, los métodos `AddTable` y `AddComputedColumn` usan el método `FillSchema` del objeto `DataAdapter` para agregar un `DataTable` a un `DataSet` y configurar el esquema para que coincida con el del origen de datos. Las propiedades extendidas agregan la información necesaria para configurar el esquema para [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 En el código de ejemplo, los métodos `AddRelation` y `AddCompositeRelation` agregan las columnas de relación, según el esquema existente y las columnas existentes en el modelo. Las columnas deben formar la parte de las tablas definidas en el esquema para que estos métodos funcionen.  
  
 El siguiente es el ejemplo de código completo:  
  
```  
static DataSourceView CreateDataSourceView(Database db, string strDataSourceName)  
{  
    // Create the data source view  
    DataSourceView dsv = db.DataSourceViews.FindByName(strDataSourceName);  
    if ( dsv != null)  
       dsv.Drop();  
    dsv = db.DataSourceViews.Add(strDataSourceName);  
    dsv.DataSourceID = strDataSourceName;  
    dsv.Schema = new DataSet();  
    dsv.Schema.Locale = CultureInfo.CurrentCulture;  
  
    // Open a connection to the data source  
    OleDbConnection connection  
        = new OleDbConnection(dsv.DataSource.ConnectionString);  
    connection.Open();  
  
    #region Create tables  
  
    // Add the DimTime table  
    AddTable(dsv, connection, "DimTime");  
    AddComputedColumn(dsv, connection, "DimTime", "SimpleDate", "DATENAME(mm, FullDateAlternateKey) + ' ' + DATENAME(dd, FullDateAlternateKey) + ',' + ' ' + DATENAME(yy, FullDateAlternateKey)");  
    AddComputedColumn(dsv, connection, "DimTime", "CalendarYearDesc", "'CY' + ' ' + CalendarYear");  
    AddComputedColumn(dsv, connection, "DimTime", "CalendarSemesterDesc", "CASE WHEN CalendarSemester = 1 THEN 'H1'+' '+ 'CY' +' '+ CONVERT(CHAR (4), CalendarYear) ELSE 'H2'+' '+ 'CY' +' '+ CONVERT(CHAR (4), CalendarYear) END");  
    AddComputedColumn(dsv, connection, "DimTime", "CalendarQuarterDesc", "'Q' + CONVERT(CHAR (1), CalendarQuarter) +' '+ 'CY' +' '+ CONVERT(CHAR (4), CalendarYear)");  
    AddComputedColumn(dsv, connection, "DimTime", "MonthName", "EnglishMonthName+' '+ CONVERT(CHAR (4), CalendarYear)");  
    AddComputedColumn(dsv, connection, "DimTime", "FiscalYearDesc", "'FY' + ' ' + FiscalYear");  
    AddComputedColumn(dsv, connection, "DimTime", "FiscalSemesterDesc", "CASE WHEN FiscalSemester = 1 THEN 'H1'+' '+ 'FY' +' '+ CONVERT(CHAR (4), FiscalYear) ELSE 'H2'+' '+ 'FY' +' '+ CONVERT(CHAR (4), FiscalYear) END");  
    AddComputedColumn(dsv, connection, "DimTime", "FiscalQuarterDesc", "'Q' + CONVERT(CHAR (1), FiscalQuarter) +' '+ 'FY' +' '+ CONVERT(CHAR (4), FiscalYear)");  
    AddComputedColumn(dsv, connection, "DimTime", "FiscalMonthNumberOfYear", "CASE WHEN MonthNumberOfYear = '1'  THEN CONVERT(int,'7') WHEN MonthNumberOfYear = '2'  THEN CONVERT(int,'8') WHEN MonthNumberOfYear = '3'  THEN CONVERT(int,'9') WHEN MonthNumberOfYear = '4'  THEN CONVERT(int,'10') WHEN MonthNumberOfYear = '5'  THEN CONVERT(int,'11') WHEN MonthNumberOfYear = '6'  THEN CONVERT(int,'12') WHEN MonthNumberOfYear = '7'  THEN CONVERT(int,'1') WHEN MonthNumberOfYear = '8'  THEN CONVERT(int,'2') WHEN MonthNumberOfYear = '9'  THEN CONVERT(int,'3') WHEN MonthNumberOfYear = '10' THEN CONVERT(int,'4') WHEN MonthNumberOfYear = '11' THEN CONVERT(int,'5') WHEN MonthNumberOfYear = '12' THEN CONVERT(int,'6') END");  
    dsv.Update();  
  
    // Add the DimGeography table  
    AddTable(dsv, connection, "DimGeography");  
  
    // Add the DimProductCategory table  
    AddTable(dsv, connection, "DimProductCategory");  
  
    // Add the DimProductSubcategory table  
    AddTable(dsv, connection, "DimProductSubcategory");  
    AddRelation(dsv, "DimProductSubcategory", "ProductCategoryKey", "DimProductCategory", "ProductCategoryKey");  
  
    // Add the DimProduct table  
    AddTable(dsv, connection, "DimProduct");  
    AddComputedColumn(dsv, connection, "DimProduct", "ProductLineName", "CASE ProductLine WHEN 'M' THEN 'Mountain' WHEN 'R' THEN 'Road' WHEN 'S' THEN 'Accessory' WHEN 'T' THEN 'Touring' ELSE 'Components' END");  
    AddRelation(dsv, "DimProduct", "ProductSubcategoryKey", "DimProductSubcategory", "ProductSubcategoryKey");  
    dsv.Update();  
  
    // Add the DimCustomer table  
    AddTable(dsv, connection, "DimCustomer");  
    AddComputedColumn(dsv, connection, "DimCustomer", "FullName", "CASE WHEN MiddleName IS NULL THEN FirstName + ' ' + LastName ELSE FirstName + ' ' + MiddleName + ' ' + LastName END");  
    AddComputedColumn(dsv, connection, "DimCustomer", "GenderDesc", "CASE WHEN Gender = 'M' THEN 'Male' ELSE 'Female' END");  
    AddComputedColumn(dsv, connection, "DimCustomer", "MaritalStatusDesc", "CASE WHEN MaritalStatus = 'S' THEN 'Single' ELSE 'Married' END");  
    AddRelation(dsv, "DimCustomer", "GeographyKey", "DimGeography", "GeographyKey");  
  
    // Add the DimReseller table  
    AddTable(dsv, connection, "DimReseller");  
    AddComputedColumn(dsv, connection, "DimReseller", "OrderFrequencyDesc", "CASE WHEN OrderFrequency = 'A' THEN 'Annual' WHEN OrderFrequency = 'S' THEN 'Bi-Annual' ELSE 'Quarterly' END");  
    AddComputedColumn(dsv, connection, "DimReseller", "OrderMonthDesc", "CASE WHEN OrderMonth = '1' THEN 'January' WHEN OrderMonth = '2' THEN 'February' WHEN OrderMonth = '3' THEN 'March' WHEN OrderMonth = '4' THEN 'April' WHEN OrderMonth = '5' THEN 'May' WHEN OrderMonth = '6' THEN 'June' WHEN OrderMonth = '7' THEN 'July' WHEN OrderMonth = '8' THEN 'August' WHEN OrderMonth = '9' THEN 'September' WHEN OrderMonth = '10' THEN 'October' WHEN OrderMonth = '11' THEN 'November' WHEN OrderMonth = '12' THEN 'December' ELSE 'Never Ordered' END");  
  
    // Add the DimCurrency table  
    AddTable(dsv, connection, "DimCurrency");  
    dsv.Update();  
  
    // Add the DimSalesReason table  
    AddTable(dsv, connection, "DimSalesReason");  
  
    // Add the FactInternetSales table  
    AddTable(dsv, connection, "FactInternetSales");  
    AddRelation(dsv, "FactInternetSales", "ProductKey", "DimProduct", "ProductKey");  
    AddRelation(dsv, "FactInternetSales", "CustomerKey", "DimCustomer", "CustomerKey");  
    AddRelation(dsv, "FactInternetSales", "OrderDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactInternetSales", "ShipDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactInternetSales", "DueDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactInternetSales", "CurrencyKey", "DimCurrency", "CurrencyKey");  
    dsv.Update();  
  
    // Add the FactResellerSales table  
    AddTable(dsv, connection, "FactResellerSales");  
    AddRelation(dsv, "FactResellerSales", "ProductKey", "DimProduct", "ProductKey");  
    AddRelation(dsv, "FactResellerSales", "ResellerKey", "DimReseller", "ResellerKey");  
    AddRelation(dsv, "FactResellerSales", "OrderDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactResellerSales", "ShipDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactResellerSales", "DueDateKey", "DimTime", "TimeKey");  
    AddRelation(dsv, "FactResellerSales", "CurrencyKey", "DimCurrency", "CurrencyKey");  
  
    // Add the FactInternetSalesReason table  
    AddTable(dsv, connection, "FactInternetSalesReason");  
    AddCompositeRelation(dsv, "FactInternetSalesReason", "FactInternetSales", "SalesOrderNumber", "SalesOrderLineNumber");  
    dsv.Update();  
  
    // Add the FactCurrencyRate table  
    AddTable(dsv, connection, "FactCurrencyRate");  
    AddRelation(dsv, "FactCurrencyRate", "CurrencyKey", "DimCurrency", "CurrencyKey");  
    AddRelation(dsv, "FactCurrencyRate", "TimeKey", "DimTime", "TimeKey");  
  
    #endregion  
  
    // Send the data source view definition to the server  
    dsv.Update();  
  
    return dsv;  
}  
  
static void AddTable(DataSourceView dsv, OleDbConnection connection, String tableName)  
{  
    string strSelectText = "SELECT * FROM [dbo].[" + tableName + "] WHERE 1=0";  
    OleDbDataAdapter adapter = new OleDbDataAdapter(strSelectText, connection);  
    DataTable[] dataTables = adapter.FillSchema(dsv.Schema,  
        SchemaType.Mapped, tableName);  
    DataTable dataTable = dataTables[0];  
  
    dataTable.ExtendedProperties.Add("TableType", "Table");  
    dataTable.ExtendedProperties.Add("DbSchemaName", "dbo");  
    dataTable.ExtendedProperties.Add("DbTableName", tableName);  
    dataTable.ExtendedProperties.Add("FriendlyName", tableName);  
  
    dataTable = null;  
    dataTables = null;  
    adapter = null;  
}  
  
static void AddComputedColumn(DataSourceView dsv, OleDbConnection connection, String tableName, String computedColumnName, String expression)  
{  
    DataSet tmpDataSet = new DataSet();  
    tmpDataSet.Locale = CultureInfo.CurrentCulture;  
    OleDbDataAdapter adapter = new OleDbDataAdapter("SELECT ("  
        + expression + ") AS [" + computedColumnName + "] FROM [dbo].["  
        + tableName + "] WHERE 1=0", connection);  
    DataTable[] dataTables = adapter.FillSchema(tmpDataSet,  
        SchemaType.Mapped, tableName);  
    DataTable dataTable = dataTables[0];  
    DataColumn dataColumn = dataTable.Columns[computedColumnName];  
  
    dataTable.Constraints.Clear();  
    dataTable.Columns.Remove(dataColumn);  
  
    dataColumn.ExtendedProperties.Add("DbColumnName", computedColumnName);  
    dataColumn.ExtendedProperties.Add("ComputedColumnExpression",  
        expression);  
    dataColumn.ExtendedProperties.Add("IsLogical", "True");  
  
    dsv.Schema.Tables[tableName].Columns.Add(dataColumn);  
  
    dataColumn = null;  
    dataTable = null;  
    dataTables = null;  
    adapter = null;  
    tmpDataSet = null;  
}  
  
static void AddRelation(DataSourceView dsv, String fkTableName, String fkColumnName, String pkTableName, String pkColumnName)  
{  
    DataColumn fkColumn  
        = dsv.Schema.Tables[fkTableName].Columns[fkColumnName];  
    DataColumn pkColumn  
        = dsv.Schema.Tables[pkTableName].Columns[pkColumnName];  
    dsv.Schema.Relations.Add("FK_" + fkTableName + "_"  
        + fkColumnName, pkColumn, fkColumn, true);  
}  
  
static void AddCompositeRelation(DataSourceView dsv, String fkTableName, String pkTableName, String columnName1, String columnName2)  
{  
    DataColumn[] fkColumns = new DataColumn[2];  
    fkColumns[0] = dsv.Schema.Tables[fkTableName].Columns[columnName1];  
    fkColumns[1] = dsv.Schema.Tables[fkTableName].Columns[columnName2];  
  
    DataColumn[] pkColumns = new DataColumn[2];  
    pkColumns[0] = dsv.Schema.Tables[pkTableName].Columns[columnName1];  
    pkColumns[1] = dsv.Schema.Tables[pkTableName].Columns[columnName2];  
  
    dsv.Schema.Relations.Add("FK_" + fkTableName + "_" + columnName1  
        + "_" + columnName2, pkColumns, fkColumns, true);  
}  
```  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.AnalysisServices>   
 [Introducción a las clases AMO](amo-classes-introduction.md)   
 [Clases fundamentales de AMO](amo-fundamental-classes.md)   
 [Arquitectura lógica &#40;Analysis Services - datos multidimensionales&#41;](../olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Objetos de base de datos &#40;Analysis Services - datos multidimensionales&#41;](../olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  

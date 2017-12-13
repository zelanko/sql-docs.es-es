---
title: "Clases complementarias de AMO y métodos de programación | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- restores [AMO]
- assemblies [AMO]
- AMO, backup and restore
- capture logs [AMO]
- programming [AMO]
- Analysis Management Objects, backup and restore
- traces [AMO]
- backups [AMO]
ms.assetid: 14aed554-d2e2-49e5-9c72-26660759bce2
caps.latest.revision: "22"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: cf80edb799a7082034d3bd359cabb42082e070ce
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="programming-amo-complementary-classes-and-methods"></a>Programar clases y métodos complementarios de AMO
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Este tema contiene las siguientes secciones:  
  
-   [Assembly (clase)](#Assembly)  
  
-   [Copias de seguridad y restauración](#BU)  
  
-   [Trace (clase)](#TRC)  
  
-   [Clase CaptureLog y atributo CaptureXML](#CL)  
  
##  <a name="Assembly"></a>Assembly (clase)  
 Ensamblados los usuarios pueden extender la funcionalidad de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] mediante la adición de nuevos procedimientos almacenados o funciones de expresiones multidimensionales (MDX). Para obtener más información, consulte [AMO otras clases y métodos](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-other-classes-and-methods.md).  
  
 Agregar y quitar ensamblados es sencillo y se puede realizar en línea. Debe ser un administrador de bases de datos para agregar un ensamblado a la base de datos o bien un administrador del servidor para agregar el ensamblado al objeto de servidor.  
  
 En el ejemplo siguiente se agrega un ensamblado a la base de datos que se proporciona y se asigna la cuenta de servicio para ejecutar el ensamblado. Si el ensamblado existe en la base de datos, se quita antes de intentar agregarlo.  
  
```  
static public void CreateStoredProcedures(Database db)  
{  
    ClrAssembly clrAssembly;  
  
    // Verify That assembly exist in database and drop it  
    if (db.Assemblies.ContainsName("StoredProcedures"))  
    {  
        clrAssembly = db.Assemblies.FindByName("StoredProcedures");  
        clrAssembly.Drop();  
    }  
  
    // Create the CLR assembly  
    clrAssembly = db.Assemblies.Add("StoredProcedures");  
    clrAssembly.ImpersonationInfo = new ImpersonationInfo(  
        ImpersonationMode.ImpersonateServiceAccount);  
    clrAssembly.PermissionSet = PermissionSet.Unrestricted;  
  
    // Load the assembly files  
    clrAssembly.LoadFiles(Environment.CurrentDirectory  
        + @"\StoredProcedures2.dll", false);  
  
    clrAssembly.Update();  
}  
  
```  
  
##  <a name="BU"></a>Métodos de restauración y copia de seguridad  
 Los métodos de copias de seguridad y restauración permiten a los administradores realizar copias de seguridad y restaurar bases de datos.  
  
 En el ejemplo siguiente se crean copias de seguridad para todas las bases de datos del servidor especificado. Si un archivo de copia de seguridad ya existe, se sobrescribe. Los archivos de copia de seguridad se guardan en la carpeta de copia de seguridad de la carpeta de datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
```  
static public void BackUpAllDatabases(Server svr)  
{  
    string fileName;  
    if ((svr != null) && ( svr.Connected))  
        foreach (Database db in svr.Databases)  
        {  
            fileName = db.Name + "_" + ((Int64)(DateTime.Today.Year * 10000 + DateTime.Today.Month * 100 + DateTime.Today.Day)).ToString()+ ".abf";  
            db.Backup(fileName, true);  
        }  
}  
```  
  
 En el ejemplo siguiente se restaura la copia de seguridad de "AdventureWorks" a partir del ejemplo anterior. Si la base de datos "My Adventure WorksDW" ya existe, se sobrescribe.  
  
```  
static public void RestoreAdventureWorks(Server svr)  
{  
    svr.Restore("Adventure Works DW_20051025.abf", "My Adventure WorksDW", true);  
}  
```  
  
##  <a name="TRC"></a>Trace (clase)  
 Al supervisar la actividad del servidor, se deben usar dos tipos de seguimientos: seguimientos de sesión y seguimientos del servidor. Realizar un seguimiento del servidor le puede indicar cómo se está realizando su tarea actual en el servidor (seguimientos de sesión) o le puede indicar el estado de la actividad total en el servidor, incluso sin estar conectado al servidor (seguimientos del servidor).  
  
 Al realizar un seguimiento de la actividad actual (seguimientos de sesión), el servidor envía notificaciones a la aplicación actual acerca de los eventos que provoca la aplicación y que se están produciendo en el servidor. Los eventos se capturan mediante controladores de eventos en la aplicación actual. En primer lugar, asigne las rutinas de control de eventos al objeto <xref:Microsoft.AnalysisServices.SessionTrace> y, a continuación, inicie el seguimiento de sesión.  
  
 En el ejemplo siguiente se muestra cómo configurar un seguimiento de sesión para realizar un seguimiento a las actividades actuales. Las rutinas de controlador de eventos se encuentran al final del ejemplo y generarán toda la información de seguimiento al objeto System.Console. Para generar eventos de seguimiento, el cubo de ejemplo "Adventure Works" se procesará totalmente una vez que se inicie el seguimiento.  
  
```  
static public void TestSessionTraces(Server svr)  
{  
    // Start the default trace  
  
    svr.SessionTrace.OnEvent  
        += new TraceEventHandler(DefaultTrace_OnEvent);  
    svr.SessionTrace.Stopped  
        += new TraceStoppedEventHandler(DefaultTrace_Stopped);  
    svr.SessionTrace.Start();  
  
    // Process the databases  
    // The trace handlers will output all progress notifications   
    // to the console  
    Database db = svr.Databases.FindByName("Adventure Works DW Multidimensional 2012");  
    Cube cube = db.Cubes.FindByName("Adventure Works");  
    cube.Process(ProcessType.ProcessFull);  
  
    // Stop the default trace  
    svr.SessionTrace.Stop();  
  
}  
static public void DefaultTrace_OnEvent(object sender, TraceEventArgs e)  
{  
    Console.WriteLine("{0}", e.TextData);  
}  
  
static public void DefaultTrace_Stopped(ITrace sender, TraceStoppedEventArgs e)  
{  
    switch (e.StopCause)  
    {  
        case TraceStopCause.StoppedByUser:  
        case TraceStopCause.Finished:  
            Console.WriteLine("Processing completed successfully");  
            break;  
  
        case TraceStopCause.StoppedByException:  
            Console.WriteLine("Processing failed: {0}",  
                e.Exception.Message);  
            break;  
    }  
}  
```  
  
 Los seguimientos del servidor se pueden configurar para registrar todo en un archivo de seguimiento y se pueden reiniciar automáticamente al reiniciar el servicio.  
  
 Para establecer un seguimiento del servidor, primero debe definir los eventos que se supervisan en el servidor y los datos del evento que se deberían guardar en el archivo de seguimiento. Para cada evento, debe definir las columnas de datos que se van a guardar en el archivo de seguimiento.  
  
 Para crear un seguimiento del servidor, es necesario realizar cuatro pasos:  
  
1.  Cree el objeto de seguimiento del servidor y rellene los atributos comunes básicos.  
  
     LogFileSize define el tamaño máximo del archivo de seguimiento y se define en megabytes; LogFileRollOver habilita al archivo de registro para que se inicie en un archivo distinto si se alcanza el límite de LogFileSize, cuando se habilita el nombre de archivo se anexa con un número de secuencia; AutoRestart permite que el seguimiento se inicie de nuevo si se reinicia el servicio.  
  
2.  Cree los eventos y las columnas de datos correspondientes.  
  
3.  Inicie y detenga el seguimiento según sea necesario.  
  
     Incluso después de que se ha detenido el seguimiento, el seguimiento existe en el servidor y se debería iniciar de nuevo si el seguimiento se ha definido como AutoRestart =**true**.  
  
4.  Quite el seguimiento cuando ya no sea necesario.  
  
 En el ejemplo siguiente, si el seguimiento ya existe, se quita y, a continuación, se vuelve a crear. Los archivos de seguimiento se guardan en la carpeta de registro de las carpetas de datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
```  
static public void TestServerTraces(Server svr)  
{  
    Trace trc;  
    TraceEvent te;  
  
        trc = svr.Traces.FindByName("TestServerTraces");  
        if (trc != null)  
            trc.Drop();  
        trc = svr.Traces.Add("TestServerTraces", "TestServerTraces");  
        trc.LogFileName = ("TestServerTraces_" +((Int64)(DateTime.Now.Year * 10000 + DateTime.Now.Month * 100 + DateTime.Now.Day)).ToString() + "_" +  
                ((Int64)(DateTime.Now.Hour * 10000 + DateTime.Now.Minute * 100 + DateTime.Now.Second)).ToString() + ".trc");  
        trc.LogFileSize = 100;  
        trc.LogFileRollover = true;  
        trc.AutoRestart = false;  
  
        #region Define Events to trace & data columns per event  
        te = trc.Events.Add(TraceEventClass.ProgressReportBegin);  
        te.Columns.Add(TraceColumn.TextData);  
        te.Columns.Add(TraceColumn.StartTime);  
        te.Columns.Add(TraceColumn.ObjectName);  
        te.Columns.Add(TraceColumn.ObjectPath);  
        te.Columns.Add(TraceColumn.DatabaseName);  
        te.Columns.Add(TraceColumn.NTCanonicalUserName);  
  
        te = trc.Events.Add(TraceEventClass.ProgressReportCurrent);  
        te.Columns.Add(TraceColumn.TextData);  
        te.Columns.Add(TraceColumn.CurrentTime);  
        te.Columns.Add(TraceColumn.ObjectName);  
        te.Columns.Add(TraceColumn.ObjectPath);  
        te.Columns.Add(TraceColumn.DatabaseName);  
  
        te = trc.Events.Add(TraceEventClass.ProgressReportEnd);  
        te.Columns.Add(TraceColumn.TextData);  
        te.Columns.Add(TraceColumn.StartTime);  
        te.Columns.Add(TraceColumn.CurrentTime);  
        te.Columns.Add(TraceColumn.EndTime);  
        te.Columns.Add(TraceColumn.Success);  
        te.Columns.Add(TraceColumn.Error);  
        te.Columns.Add(TraceColumn.ObjectName);  
        te.Columns.Add(TraceColumn.ObjectPath);  
        te.Columns.Add(TraceColumn.DatabaseName);  
        te.Columns.Add(TraceColumn.NTCanonicalUserName);  
        #endregion  
  
        trc.Update();  
        trc.Start();  
  
        #region Process the Adventure Works Cube  
        // The trace settings will output all progress notifications   
        // to the trace file  
        Database db = svr.Databases.FindByName("Adventure Works DW Multidimensional 2012");  
        Cube cube = db.Cubes.FindByName("Adventure Works");  
        cube.Process(ProcessType.ProcessFull);  
        #endregion  
  
        trc.Stop();  
        trc.Drop();  
  
}  
```  
  
##  <a name="CL"></a>Atributos CaptureLog y CaptureXml  
 El atributo CaptureLog le habilita para crear archivos por lotes XMLA a partir de sus operaciones AMO. CaptureLog le habilita para crear un script para objetos de servidor como bases de datos, cubos, dimensiones, estructuras de minería de datos, etc.  
  
 Para crear CaptureLog, es necesario realizar los pasos siguientes:  
  
1.  Iniciar la captura del registro XMLA estableciendo el servidor de atributo CaptureXml a **true**.  
  
     Esta opción empezará a guardar todas las operaciones AMO en una colección de cadenas en lugar de enviarlas al servidor.  
  
2.  Inicie la actividad AMO de la manera habitual, pero recuerde que no se envía ninguna acción al servidor. La actividad puede ser cualquier operación como procesar, crear, eliminar, actualizar o cualquier otra acción sobre un objeto.  
  
3.  Detener la captura del registro XMLA restableciendo CaptureXml a **false**.  
  
4.  Revise el XMLA capturado, revisando cada una de las cadenas de la colección de cadenas CaptureLog o bien generando una cadena completa con el método ConcatenateCaptureLog. ConcatenateCaptureLog le habilita para generar el lote XMLA como una transacción única y agregar la opción de proceso paralela al lote.  
  
 En el ejemplo siguiente se devuelve una cadena con los comandos de proceso por lotes necesarios para realizar un proceso completo en todas las dimensiones y en todos los cubos de la base de datos [Adventure Works DW Multidimensional 2012].  
  
```  
static public string TestCaptureLog(Server svr)  
{  
    String capturedXmla = "";  
    if ((svr != null) && (svr.Connected))  
    {  
        svr.CaptureXml = true;  
  
        #region Actions to be captured to an XMLA file  
        //No action is executed during CaptureXml = true  
        Database db = svr.Databases.FindByName("Adventure Works DW Multidimensional 2012");  
        foreach (Dimension dim in db.Dimensions)  
            dim.Process(ProcessType.ProcessFull);  
        foreach (Cube cube in db.Cubes)  
            cube.Process(ProcessType.ProcessFull);  
        #endregion  
  
        svr.CaptureXml = false;  
  
        capturedXmla = svr.ConcatenateCaptureLog(true, true);  
  
    }  
  
    return capturedXmla;  
}  
```  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.AnalysisServices>   
 [Introducción a las clases AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [AMO otras clases y métodos](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-other-classes-and-methods.md)   
 [Arquitectura lógica &#40; Analysis Services - datos multidimensionales &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Objetos de base de datos &#40; Analysis Services - datos multidimensionales &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [Procesar un modelo multidimensional &#40; Analysis Services &#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  

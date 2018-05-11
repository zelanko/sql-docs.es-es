---
title: Instalar, distribuir y hacer referencia al modelo de objeto Tabular | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 81f3b12aeb7cb6a185c0ee9b1152d75f3451c4b0
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="install-distribute-and-reference-the-tabular-object-model"></a>Instalar, distribuir y hacer referencia al modelo de objeto Tabular
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
En este artículo se explica cómo descargar, hacer referencia y redistribuir Analysis Services Tabular objeto modelo (TOM), una biblioteca de C# para crear y administrar los modelos tabulares y las bases de datos en código administrado.  
  
TOM es una extensión de la biblioteca de cliente AMO (Microsoft.AnalysisServices.dll) que se incluye con SQL Server 2016. Funciona con los modelos tabulares que se elige como destino el motor de metadatos tabulares en la versión de SQL Server 2016. Para usar TOM, el modelo y la base de datos deben estar en el nivel de compatibilidad 1200 o superior.  

## <a name="amo-tom-assemblies"></a>Ensamblados de TOM de AMO

SQL Server 2016 refactoriza y expande AMO para incluir nuevos ensamblados principales, Tabular y JSON. También incluye el ensamblado original de AMO, Microsoft.AnalysisServices.dll, que se ha formado parte de Analysis Services desde la primera versión. Un AMO reestructurado descarga clases comunes a un ensamblado y proporciona una división lógica entre tabulares y multidimensionales de las API a través de ensamblados adicionales. 

En la tabla siguiente describe cada ensamblado.
  
Ensamblado  |Funcionalidad  |Clases importantes |
---------|---------|--------------  |
Core <br/>Microsoft.AnalysisServices.Core.dll | Comunes a las bases de datos tabulares y multidimensionales. <br/><br/>Proporciona control de excepciones, genéricas conexiones a una instancia de Analysis Services y la base de datos y el acceso a propiedades y métodos comunes para objetos de servidor y base de datos. <br/><br/>Se requiere para cualquier solución AMO como destino SQL Server 2016. | Core&nbsp;Server<br/>Core&nbsp;base de datos<br/>AmoException
TOM<br/> Microsoft.AnalysisServices.Tabular.dll, versión 13.0.1601.5 o posterior.| Crear y administrar objetos de metadatos tabulares. | TOM&nbsp;Server <br/>TOM&nbsp;base de datos<br /> Modelo<br /> Table<br /> Columna<br /> Relación
  AMO<br /> Microsoft.AnalysisServices.dll| Crear y administrar objetos de metadatos multidimensionales, incluidas bases de datos Tabular 1050-1103. | AMO&nbsp;Server <br />AMO&nbsp;base de datos <br /> Cube <br /> Dimensión <br /> MeasureGroup 
JSON<br/>Microsoft.AnalysisServices.Tabular.Json.dll | Una aplicación auxiliar de DLL que encapsula el NewtonSoftJson.dll (JSON.NET) para controlar las actualizaciones, se evita el riesgo de introducir cambios funcionales para la serialización de JSON en las cargas de trabajo de Analysis Services. <br /> <br />Este archivo DLL existe como una dependencia en TOM y no está diseñada para utilizarse directamente en el código. | Ninguno.  
  
 ### <a name="understanding-assembly-dependencies"></a>Descripción de las dependencias de ensamblado
  
Para programar con AMO, la solución debe incluir referencias a archivos DLL dependientes. AMO y TOM dependen Core porque proporciona clases base.

AMO depende de TOM porque algunas clases de AMO hacen referencia a las clases de TOM. Por ejemplo, el objeto de base de datos de AMO tiene una propiedad de modelo de tipo modelo, que se implementa en el archivo dll de TOM. 

![Dependencias de AMO TOM](../../analysis-services/tabular-model-programming-compatibility-level-1200/media/amo-tom-dependencies.png)

No se puede distribuir Microsoft.AnalysisServices.dll sin Microsoft.AnalysisServices.Tabular.dll, pero puede hacer referencia a sus respectivos espacios de nombres sin el otro.

### <a name="choosing-which-namespace-to-use-in-code"></a>Elegir qué espacio de nombres para utilizar en el código

En el [jerarquía del objeto](../../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md) , cualquier objeto de base de datos es una construcción de metadatos tabulares a través del objeto de modelo o una construcción de metadatos multidimensionales a través de un objeto de cubo, dimensión o MeasureGroup. Para las operaciones de alto nivel en el nivel de servidor, base de datos, rol o seguimiento, debe admitir la elección de qué espacio de nombres para hacer referencia a dependerá de las cargas de trabajo del código.

* Use Tabular.Server o Tabular.Database si la solución es el nivel de compatibilidad 1200 o superior, y trabajar con el objeto de base de datos debe proporcionar acceso al modelo, tabla, columnas y otros objetos expresadas como construcciones de metadatos tabulares.
* Use AnalysisServices.Server o AnalysisServices.Database si objetos multidimensionales, como cubos, orígenes de datos, DataSourceViews y dimensiones hace referencia a código de nivel inferior.

Necesitará dos espacios de nombres para herramientas y aplicaciones que admiten una mezcla de las bases de datos y tipos de modelo. 

Referencia de espacio de nombres principal en el código no es necesario; las clases de núcleo son clases base creadas con el fin de proporcionar propiedades comunes, como el nombre y la descripción de los objetos principales.  
  
## <a name="determine-whether-amo-and-tom-installation-is-required"></a>Determinar si es necesaria la instalación de AMO y TOM  
   
 AMO y TOM se agrupan en una biblioteca de cliente único. Si ya instaló una instancia de SQL Server 2016 Analysis Services, las bibliotecas de cliente o una versión de SQL Server Data Tools destinado a una instancia de 2016 de SQL Server, el archivo Microsoft.AnalysisServices.dll ya está instalado.  
  
 Para determinar si los ensamblados ya están instalados, consulte cualquiera de estas ubicaciones:
* C:\Windows\Microsoft.NET\assembly\GAC_MSIL
* C:\Program Files\Microsoft SQL Server\130\SDK\Assemblies
* C:\Program Files\Microsoft SQL Server\130\DTS\Tasks
* C:\Program Files\Microsoft SQL Server\MSAS13. MSSQLSERVER\OLAP\bin
 
 Compruebe que existen los siguientes ensamblados:
*  Microsoft.AnalysisServices.Core.dll
*  Microsoft.AnalysisServices.dll
*  Microsoft.AnalysisServices.Tabular.dll
*  Microsoft.AnalysisServices.Tabular.Json.dll   
   
## <a name="download-sqlasamo"></a>Descargar SQL_AS_AMO  
 
 Tenga en cuenta que no está disponible a través del Administrador de NuGet Microsoft.AnalysisServices.dll.
  
1. Vaya a [página de descarga de SQL Server 2016 Feature Pack](https://www.microsoft.com/download/details.aspx?id=52676).  
  
2. Haga clic en **Descargar**.  
  
3. Seleccione **\X64\SQL_AS_AMO.msi** o **\X86\SQL_AS_AMO.msi**. Puede elegir cualquiera de ellos: AMO y TOM ensamblados son independientes de la plataforma.
  
4. Haga clic en **siguiente** para continuar con la descarga. Encontrará los archivos .msi en su **descarga** carpeta.  
  
## <a name="install-sqlasamo"></a>Instalar SQL_AS_AMO  
  
1. Haga doble clic en **SQL_AS_AMO.msi** y paso a través de la instalación.  
  
2. Vaya a **C:\Program Files\Microsoft SQL Server\130\SDK\Assemblies** para confirmar la selección de ubicación de Microsoft.AnalysisServices.Core.dll, Microsoft.AnalysisServices.dll, Microsoft.AnalysisServices.Tabular.dll, y Microsoft.AnalysisServices.Tabular.Json.dll.   
  
## <a name="add-references"></a>Agregar referencias  
  
1. En **el Explorador de soluciones** > **Agregar referencia** > **examinar**.  
2. Vaya a **C:\Program Files\Microsoft SQL Server\130\SDK\Assemblies** y seleccione:  
   * Microsoft.AnalysisServices.Core  
   * Microsoft.AnalysisServices.Tabular  
   * Microsoft.AnalysisSerivces.Tabular.Json  
  
3. Haga clic en **Aceptar**.  En **el Explorador de soluciones**, asegúrese de los ensamblados se encuentran en la carpeta de referencias.
  
4. En la página de códigos, agregue el espacio de nombres Microsoft.AnalysisServices.tabular si hay bases de datos y modelos tabulares de 1200 o nivel de compatibilidad superior. 
  
   ```   
   using Microsoft.AnalysisServices; 
   using Microsoft.AnalysisServices.Tabular;
   ```  
    Opcionalmente, agregue Microsoft.AnalysisServces para admitir un conjunto más amplio de conexiones con instancias de Analysis Services que no sean específicamente SQL Server 2016 en modo de servidor Tabular. 
 
    Cuando se incluyen los espacios de nombres que tienen en común las clases de objetos de servidor, base de datos, roles y seguimiento, evite las referencias ambiguas calificando qué espacio de nombres que se va a utilizar (por ejemplo, Microsoft.AnalysisServices.Tabular.Server crea una instancia de un servidor objeto con el espacio de nombres Tabular).

## <a name="redistribute-amo-and-tom-with-your-application"></a>Redistribuir AMO y TOM con la aplicación  
  
La redistribución de AMO y TOM es a través de la **sql_as_amo.msi** paquete de instalación. Si está generando un programa de instalación para una aplicación cliente que llama en AMO o TOM, agregue **sql_as_amo.msi** a su archivo ejecutable. Este es el único mecanismo compatible para redistribuir las bibliotecas de cliente AMO y TOM.  
  
El paquete es independiente entre sí y proporciona todos los ensamblados necesarios para llamar a AMO y TOM en el código. Otros paquetes, como SQL_AS_OLEDB.msi o SQL_AS_ADOMD.msi, no son necesarios específicamente para escenarios de programación de TOM.

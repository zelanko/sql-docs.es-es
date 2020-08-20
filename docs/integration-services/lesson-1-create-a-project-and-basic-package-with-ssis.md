---
description: 'Lección 1: Creación de un proyecto y un paquete básico con SSIS'
title: 'Lección 1: Creación de un proyecto y un paquete básico con SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 84d0b877-603f-4f8e-bb6b-671558ade5c2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 428295430a2abb50738742db088b9573a7bf35a6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461999"
---
# <a name="lesson-1-create-a-project-and-basic-package-with-ssis"></a>Lección 1: Creación de un proyecto y un paquete básico con SSIS

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



En esta lección, se crea un paquete ETL sencillo que extrae datos de un único origen de archivo plano, los transforma mediante dos componentes de transformación de búsqueda y escribe los datos transformados en una copia de la tabla de hechos **FactCurrencyRate** de la base de datos de muestra **AdventureWorksDW2012**. Como parte de esta lección, aprenderá a crear paquetes, agregar y configurar orígenes de datos y conexiones de destino, y trabajar con nuevos componentes de flujo de control y flujo de datos.  
  
Antes de crear un paquete, debe entender el formato que se usa en los datos de origen y de destino. Después, estará listo para definir las transformaciones necesarias para asignar los datos de origen al destino.  

## <a name="prerequisites"></a>Requisitos previos

Este tutorial se basa en Microsoft SQL Server Data Tools, un conjunto de paquetes de ejemplo y una base de datos de ejemplo.

* Para instalar SQL Server Data Tools, vea [Descargar SQL Server Data Tools](../ssdt/download-sql-server-data-tools-ssdt.md).  
  
* Para descargar todos los paquetes de la lección de este tutorial:

    1.  Vaya a los [archivos de tutorial de Integration Services](https://www.microsoft.com/download/details.aspx?id=56827).

    2.  Haga clic en el botón **DOWNLOAD** (DESCARGAR).

    3.  Seleccione **Creating a Simple ETL Package.zip** (Creación de un sencillo archivo Package.zip de ETL) y, después, haga clic en **Next** (Siguiente).

    4.  Después de que se descargue el archivo, descomprima el contenido en un directorio local.  

* Para instalar e implementar la base de datos de ejemplo **AdventureWorksDW2012**, vea [Configuración e instalación de AdventureWorks](../samples/adventureworks-install-configure.md).
  
## <a name="look-at-the-source-data"></a>Examen de los datos de origen
En este tutorial, los datos de origen son un conjunto de datos de moneda históricos que se encuentra en un archivo plano denominado **SampleCurrencyData.txt**. Los datos de origen tienen las cuatro columnas siguientes: tipo de cambio medio de la moneda, una clave de moneda, una clave de fecha y el tipo de cambio de final del día.  
  
Este es un ejemplo de los datos de origen del archivo SampleCurrencyData.txt:  
  
```
1.00070049USD9/3/05 0:001.001201442  
1.00020004USD9/4/05 0:001  
1.00020004USD9/5/05 0:001.001201442  
1.00020004USD9/6/05 0:001  
1.00020004USD9/7/05 0:001.00070049  
1.00070049USD9/8/05 0:000.99980004  
1.00070049USD9/9/05 0:001.001502253  
1.00070049USD9/10/05 0:000.99990001  
1.00020004USD9/11/05 0:001.001101211  
1.00020004USD9/12/05 0:000.99970009
```
  
Cuando se trabaja con datos de origen de un archivo plano, es importante entender el modo en el que el administrador de conexiones de archivos planos interpreta los datos del archivo plano. Si el origen de archivo plano es Unicode, el administrador de conexiones de archivos planos define todas las columnas como [DT_WSTR], con un ancho de columna predeterminado de 50. Si el origen de archivo plano tiene la codificación ANSI, las columnas se definen como [DT_STR], con un ancho de columna predeterminado de 50. Es probable que tenga que cambiar estos valores predeterminados para que los tipos de columna de cadena sean más adecuados para los datos. Debe examinar el tipo de datos de destino y, después, elegir ese tipo en el Administrador de conexiones de archivos planos.  
  
## <a name="look-at-the-destination-data"></a>Examen de los datos de destino
El destino de los datos de origen es una copia de la tabla de hechos **FactCurrencyRate** de **AdventureWorksDW**. La tabla de hechos **FactCurrencyRate** tiene cuatro columnas y tiene relaciones con dos tablas de dimensiones, como se muestra en la tabla siguiente.  
  
|Nombre de columna|Tipo de datos|Tabla de búsqueda|columna de búsqueda|  
|---------------|-------------|----------------|-----------------|  
|AverageRate|FLOAT|None|None|  
|CurrencyKey|int (FK)|DimCurrency|CurrencyKey (PK)|  
|DateKey|int (FK)|DimDate|DateKey (PK)|  
|EndOfDayRate|FLOAT|None|None|  
  
## <a name="map-the-source-data-to-the-destination"></a>Asignación de los datos de origen al destino  
El análisis de los formatos de datos de origen y de destino indica que se necesitan búsquedas para los valores **CurrencyKey** y **DateKey**. Las transformaciones que realizan estas búsquedas obtienen esos valores mediante las claves alternativas de las tablas de dimensiones **DimCurrency** y **DimDate**.  
  
|Columna de archivo plano|Nombre de la tabla|Nombre de columna|Tipo de datos|  
|--------------------|--------------|---------------|-------------|  
|0|FactCurrencyRate|AverageRate|FLOAT|  
|1|DimCurrency|CurrencyAlternateKey|nchar (3)|  
|2|DimDate|FullDateAlternateKey|date|  
|3|FactCurrencyRate|EndOfDayRate|FLOAT|  
  
## <a name="lesson-tasks"></a>Tareas de la lección  
Esta lección contiene las siguientes tareas:  
  
-   [Paso 1: Crear un nuevo proyecto de Integration Services](../integration-services/lesson-1-1-creating-a-new-integration-services-project.md)  
  
-   [Paso 2: Incorporación y configuración de un administrador de conexiones de archivos planos](../integration-services/lesson-1-2-adding-and-configuring-a-flat-file-connection-manager.md)  
  
-   [Paso 3: Adición y configuración de un administrador de conexiones OLE DB](../integration-services/lesson-1-3-adding-and-configuring-an-ole-db-connection-manager.md)  
  
-   [Paso 4: Adición de una tarea de flujo de datos al paquete](../integration-services/lesson-1-4-adding-a-data-flow-task-to-the-package.md)  
  
-   [Paso 5: Adición y configuración del origen de archivo plano](../integration-services/lesson-1-5-adding-and-configuring-the-flat-file-source.md)  
  
-   [Paso 6: Adición y configuración de las transformaciones de búsqueda](../integration-services/lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
-   [Paso 7: Adición y configuración del destino de OLE DB](../integration-services/lesson-1-7-adding-and-configuring-the-ole-db-destination.md)  
  
-   [Paso 8: Anotación y formato del paquete de la lección 1](../integration-services/lesson-1-8-making-the-lesson-1-package-easier-to-understand.md)  
  
-   [Paso 9: Prueba del paquete de la lección 1](../integration-services/lesson-1-9-testing-the-lesson-1-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar la lección  
[Paso 1: Creación de un proyecto de Integration Services](../integration-services/lesson-1-1-creating-a-new-integration-services-project.md)  
  

---
title: "Importación de archivos planos en SQL | Microsoft Docs"
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-non-specified
ms.reviewer: douglasl
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.importflatfile.f1
author: yualan
ms.author: alayu
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 3180456162da02ecef897fd340663500792d4785
ms.contentlocale: es-es
ms.lasthandoff: 10/10/2017

---
# <a name="import-flat-file-to-sql-wizard"></a>Importación de archivos planos mediante el asistente de SQL
> Para obtener más información sobre el Asistente para importación y exportación, consulte [Asistente para importación y exportación de SQL Server](https://docs.microsoft.com/en-us/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard).

El Asistente para importación de archivos planos es una forma muy sencilla de copiar datos de un archivo plano (.csv, .txt) en un destino determinado. En la información general puede consultar los motivos por los que el asistente resulta tan útil, el proceso para encontrarlo y un ejemplo que podrá seguir fácilmente.

## <a name="why-would-i-use-this-wizard"></a>¿Por qué el asistente es tan útil?
El objetivo del asistente es mejorar la experiencia de importación actual y ofrece un marco inteligente conocido como Program Synthesis using Examples ([PROSE](https://microsoft.github.io/prose/)). Para un usuario sin conocimientos especializados en el tema de los dominios, importar datos puede ser una tarea compleja y tediosa, además de que se suelen producir errores. Este asistente permite simplificar el proceso de importación, ya que basta con seleccionar un archivo de entrada y un nombre de tabla único. El marco de PROSE se encarga del resto.

PROSE analiza los patrones de datos del archivo de entrada e infiere los nombres de las columnas, los tipos y los delimitadores, entre otros valores. El marco memoriza la estructura del archivo y hace el resto del trabajo para que los usuarios no tengan que preocuparse de ello.

## <a name="prerequisites"></a>Requisitos previos
Esta característica solo está disponible para la versión 17.3 de SQL Server Management Studio (SSMS) u otras posteriores. Asegúrese de utilizar la última versión, que podrá encontrar [aquí](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).
 
## <a id="started"></a>Introducción
Para acceder al Asistente para importación de archivos planos, siga estos pasos:

1. Abra **SQL Server Management Studio**.
2. Conéctese a una instancia de Motor de base de datos de SQL Server o el localhost.
3. Expanda **Bases de datos**, haga clic con el botón derecho en una base de datos (vea el ejemplo siguiente), apunte a **Tareas** y haga clic en **Importar archivo plano**, encima de Importar datos.

![Menú del asistente](media/import-flat-file-wizard/importffmenu.png)

Para obtener más información sobre las diferentes funciones del asistente, consulte el tutorial siguiente.

## <a name="tutorial"></a>Tutorial
Dados los objetivos que se contemplan en este tutorial, puede usar un archivo plano propio. En caso contrario, en este tutorial se usará el siguiente archivo .csv de Excel que puede copiar sin ningún problema. Si decide usar dicho archivo .csv, llámelo **ejemplo.csv** y guárdelo como .csv en una ubicación que pueda encontrar fácilmente, por ejemplo, el escritorio.

![Asistente: Excel](media/import-flat-file-wizard/importffexample.png)

### <a name="step-1-access-wizard-and-intro-page"></a>Paso 1: acceso al asistente y página de introducción
Acceda al asistente tal y como se describe [aquí](#started).

La primera página del asistente es la página principal. Si no quiere que se vuelva a mostrar, haga clic en **No volver a mostrar esta página**.

![Asistente: introducción](media/import-flat-file-wizard/importffintro.png)

### <a name="step-2-specify-input-file"></a>Paso 2: especificación del archivo de entrada
Haga clic en Examinar y seleccione el archivo de entrada. De forma predeterminada, el asistente buscará archivos .csv y .txt. 

El nuevo nombre de la tabla debe ser único, ya que, en caso contrario, el asistente no le permitirá avanzar.

![Asistente: especificación](media/import-flat-file-wizard/importffspecify.png)

### <a name="step-3-preview-data"></a>Paso 3: vista previa de los datos
El asistente generará una vista previa para que pueda consultar las primeras 50 filas. Si hay algún problema, haga clic en Cancelar. Si no, proceda a la página siguiente.

![Asistente: vista previa](media/import-flat-file-wizard/importffpreview.png)

### <a name="step-4-modify-columns"></a>Paso 4: modificación de las columnas
El asistente identificará lo que en teoría son los nombres de columnas, los tipos de datos, etc. En caso de que los campos no sean correctos, en este paso podrá editarlos, por ejemplo, si el tipo de datos debe ser "float" en lugar de "int".

Una vez que todo sea correcto, continúe.

![Asistente: modificación](media/import-flat-file-wizard/importffmodify.png)

### <a name="step-5-summary"></a>Paso 5: resumen
Esta página es simplemente un resumen en el que figura la configuración actual. Si hay algún problema puede volver a las secciones anteriores. Si no los hay, haga clic en Finalizar para intentar efectuar la importación.

![Asistente: resumen](media/import-flat-file-wizard/importffsummary.png)

### <a name="step-6-results"></a>Paso 6: resultados
En esta página se indica si la importación se ha realizado correctamente. Si la operación se ha efectuado correctamente, aparecerá una marca de verificación verde. De lo contrario, deberá comprobar que no haya errores con los archivos de entrada o con la configuración.

![Asistente: resultados](media/import-flat-file-wizard/importffresults.png)

## <a name="learn-more"></a>Más información

Obtenga más información sobre el asistente.

- **Obtenga más información sobre cómo importar otros orígenes**. Si quiere importar otros recursos además de archivos planos, consulte [Asistente para importación y exportación de SQL Server](https://docs.microsoft.com/en-us/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard).
- **Obtenga más información sobre cómo conectar con orígenes de archivos planos**. Si quiere más información sobre cómo conectar con orígenes de archivos planos, consulte [Connect to a Flat File Data Source](https://docs.microsoft.com/en-us/sql/integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard) (Conexión con orígenes de datos de archivos planos).
- **Obtenga más información sobre PROSE**. Si quiere información general sobre el marco inteligente que usa este asistente, consulte [PROSE SDK](https://microsoft.github.io/prose/) (SDK de PROSE).



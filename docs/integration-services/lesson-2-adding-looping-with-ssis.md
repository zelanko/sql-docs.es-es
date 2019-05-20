---
title: 'Lección 2: Adición de bucles con SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 01f2ed61-1e5a-4ec6-b6a6-2bd070c64077
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e8903517affd4d0a8e395a17cb97e27ddd5a67d5
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/16/2019
ms.locfileid: "65722447"
---
# <a name="lesson-2-add-looping-with-ssis"></a>Lección 2: Adición de bucles con SSIS

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



En la [Lección 1: Creación de un proyecto y paquete básico con SSIS](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md), ha creado un paquete que extrae datos de un único origen de archivo plano. Después, los datos se han transformado mediante transformaciones de búsqueda. Por último, el paquete carga los datos en una copia de la tabla de hechos **FactCurrencyRate** de la base de datos de ejemplo **AdventureWorksDW2012**.  
  
En un proceso de extracción, transformación y carga (ETL), los datos se suelen extraer de varios orígenes de archivos planos. Para extraer datos de varios orígenes, se requiere un flujo de control iterativo. [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] puede agregar fácilmente iteración o bucles a los paquetes.  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] proporciona dos tipos de contenedores para crear bucles en los paquetes: el contenedor de bucles Foreach y el contenedor de bucles For. El contenedor de bucles Foreach usa un enumerador para el bucle, mientras que el contenedor de bucles For suele usar una expresión variable. En esta lección se utiliza el contenedor de bucles Foreach.  
  
El contenedor de bucles Foreach permite que un paquete repita el flujo de control para cada miembro de un enumerador determinado. Con el contenedor de bucles Foreach puede enumerar lo siguiente:  
  
-   Filas de conjuntos de registros ADO  
  
-   Información del esquema de ADO .Net  
  
-   Estructuras de archivos y directorios  
  
-   Variables del sistema, de paquete y de usuario  
  
-   Objetos enumerables de una variable  
  
-   Elementos de una colección  
  
-   Nodos de una expresión del lenguaje de rutas XML (XPath)  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Objetos de administración (SMO)  
  
En esta lección, se modifica el paquete ETL de ejemplo de la lección 1 para usar un contenedor de bucles Foreach, y se establece una variable de paquete definida por el usuario para el paquete. Después, se usa esa variable para recorrer en iteración los archivos coincidentes en la carpeta de ejemplo.   
  
En esta lección, no modificará el flujo de datos, solamente modificará el de control.  
  
> [!NOTE]  
> Si todavía no lo ha hecho, vea los [requisitos previos de la lección 1](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites).

## <a name="lesson-tasks"></a>Tareas de la lección  
Esta lección contiene las siguientes tareas:  
  
-   [Paso 1: Copia del paquete de la lección 1](../integration-services/lesson-2-1-copying-the-lesson-1-package.md)  
  
-   [Paso 2: Adición y configuración del contenedor de bucles Foreach](../integration-services/lesson-2-2-adding-and-configuring-the-foreach-loop-container.md)  
  
-   [Paso 3: Modificación del Administrador de conexiones de archivos planos](../integration-services/lesson-2-3-modifying-the-flat-file-connection-manager.md)  
  
-   [Paso 4: Prueba del paquete del tutorial de la lección 2](../integration-services/lesson-2-4-testing-the-lesson-2-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar la lección  
[Paso 1: Copia del paquete de la lección 1](../integration-services/lesson-2-1-copying-the-lesson-1-package.md)  
  
## <a name="see-also"></a>Vea también  
[Contenedor de bucles For](../integration-services/control-flow/for-loop-container.md)  
  
  
  

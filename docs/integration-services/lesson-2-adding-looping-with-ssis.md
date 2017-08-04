---
title: "Lección 2: Agregar bucles con SSIS | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 01f2ed61-1e5a-4ec6-b6a6-2bd070c64077
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8559dc3afb5f347555b9b21b61abc50765fd92c4
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="lesson-2-adding-looping-with-ssis"></a>Lección 2: Agregar bucles con SSIS
En la [Lección 1: Crear el proyecto y el paquete básico](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md), creó un paquete que extraía datos de un solo origen de archivo plano, transformó los datos mediante transformaciones de búsqueda y, por último, cargó los datos en la tabla de hechos **FactCurrency** de la base de datos de ejemplo **AdventureWorksDW2012** .  
  
No obstante, no es muy habitual utilizar un solo archivo plano para el proceso de extracción, transformación y carga (ETL). Un proceso ETL típico utilizaría datos extraídos de varios orígenes de archivos planos. Para extraer datos de varios orígenes, se requiere un flujo de control iterativo. Una de las características más esperadas de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] es la capacidad de agregar fácilmente una iteración o un bucle a los paquetes.  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] proporciona dos tipos de contenedores para crear bucles en los paquetes: el contenedor de bucles Foreach y el contenedor de bucles For. El contenedor de bucles Foreach usa un enumerador para crear el bucle, mientras que el contenedor de bucles For suele emplear una expresión variable. En esta lección se utiliza el contenedor de bucles Foreach.  
  
El contenedor de bucles Foreach permite que un paquete repita el flujo de control para cada miembro de un enumerador determinado. Con el contenedor de bucles Foreach puede enumerar lo siguiente:  
  
-   Filas de conjuntos de registros ADO  
  
-   Información del esquema de ADO .Net  
  
-   Estructuras de archivos y directorios  
  
-   Variables del sistema, de paquete y de usuario  
  
-   Objetos enumerables contenidos en una variable  
  
-   Elementos de una colección  
  
-   Nodos de una expresión del lenguaje de rutas XML (XPath)  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Objetos de administración (SMO)  
  
En esta lección, modificará el paquete ETL simple creado en la lección 1 para beneficiarse del contenedor de bucles Foreach. También establecerá variables de paquete definidas por el usuario para que el paquete del tutorial pueda iterarse en todos los archivos planos de la carpeta. Si no ha finalizado la lección anterior, también puede copiar el paquete de la lección 1 finalizada incluido en el tutorial.  
  
En esta lección, no modificará el flujo de datos, solamente modificará el flujo de control.  
  
> [!IMPORTANT]  
> Para este tutorial, se necesita la base de datos de ejemplo **AdventureWorksDW2012** . Para obtener más información sobre cómo instalar e implementar **AdventureWorksDW2012**, consulte [Ejemplos de productos de Reporting Services en CodePlex](http://go.microsoft.com/fwlink/p/?LinkID=526910).  
  
## <a name="lesson-tasks"></a>Tareas de la lección  
Esta lección contiene las siguientes tareas:  
  
-   [Paso 1: copiar el paquete de la lección 1](../integration-services/lesson-2-1-copying-the-lesson-1-package.md)  
  
-   [Paso 2: agregar y configurar el contenedor de bucles Foreach](../integration-services/lesson-2-2-adding-and-configuring-the-foreach-loop-container.md)  
  
-   [Paso 3: Modificar el Administrador de conexiones de archivos planos](../integration-services/lesson-2-3-modifying-the-flat-file-connection-manager.md)  
  
-   [Paso 4: Probar el paquete del tutorial de la lección 2](../integration-services/lesson-2-4-testing-the-lesson-2-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar la lección  
[Paso 1: copiar el paquete de la lección 1](../integration-services/lesson-2-1-copying-the-lesson-1-package.md)  
  
## <a name="see-also"></a>Vea también  
[Contenedor de bucles For](../integration-services/control-flow/for-loop-container.md)  
  
  
  


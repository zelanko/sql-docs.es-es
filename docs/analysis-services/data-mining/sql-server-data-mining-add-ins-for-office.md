---
title: Los datos de SQL Server a los complementos de minería de datos para Office | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 89986d3c8de4a1cbefbccf285a92a2dc19c6c7aa
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52504746"
---
# <a name="sql-server-data-mining-add-ins-for-office"></a>Complementos de minería de datos de SQL Server para Office

  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Complementos de minería de datos para Office es un conjunto ligero de herramientas para análisis predictivos que permite utilizar datos de Excel para generar modelos analíticos para la predicción, recomendación o exploración.  
  
> [!IMPORTANT]
> El complemento de minería de datos con datos para Office no se admite en Office 2016 o posterior.
  
 Los asistentes y las herramientas de administración de datos de los complementos proporcionan instrucciones paso a paso para estas tareas comunes de minería de datos:  
  
-   **Organizar y limpiar los datos antes del modelado.** Utilice los datos almacenados en Excel o en cualquier origen de datos de Excel. Puede crear y guardar las conexiones para reutilizar los orígenes de datos y repetir experimentos o volver a entrenar los modelos.  
  
-   **Generar perfiles, obtener muestras y preparar los datos.** Muchos mineros de datos experimentados afirman que el 70-90 por ciento de un proyecto de minería de datos se emplea en la preparación de los datos. Los complementos pueden agilizar esta tarea, proporcionando visualizaciones de Excel y asistentes que le ayudan en estas tareas comunes:  
  
    -   Realizar el perfil de los datos y comprender su distribución y sus características.  
  
    -   Crear conjuntos de entrenamiento y pruebas con el muestreo aleatorio o el sobremuestreo.  
  
    -   Buscar los valores atípicos y suprimirlos o reemplazarlos.  
  
    -   Cambiar la etiqueta de los datos para mejorar la calidad del análisis.  
  
-   **Analizar patrones a través de aprendizaje supervisado o no supervisado.** Desplácese haciendo clic por sencillos asistentes para realizar algunas de las tareas de minería de datos más populares, incluidos el análisis de agrupación en clústeres, el análisis de la cesta de compras y el pronóstico.  
  
     Entre los algoritmos de aprendizaje automático conocidos incluidos en los complementos están Naïve Bayes, regresión logística, clústeres, serie temporal y redes neuronales.  
  
     Si no está familiarizado con la minería de datos, puede obtener ayuda sobre la generación de consultas de predicción en el asistente **Consulta** .  
  
     Los usuarios avanzados pueden crear consultas DMX personalizadas con el **Editor de consultas avanzadas**que permite arrastrar y colocar, o automatizar las predicciones con VBA de Excel.  
  
-   **Documentar y administrar.** Una vez que ha creado un conjunto de datos y generar algunos modelos, documente el trabajo y sus conocimientos mediante la generación de un resumen estadístico de los parámetros de datos y el modelo.  
  
-   **Explorar y visualizar.** Minería de datos no es una actividad que se puede automatizar completamente: necesita explorar y entender los resultados para realizar las acciones adecuadas. Los complementos le ayudan con la exploración al proporcionar visores interactivos de Excel, plantillas de Visio que le permiten personalizar los diagramas de modelos y la capacidad de exportar los gráficos y las tablas de Excel para filtrarlas o modificarlas más.  
  
-   **Implementar e integrar.** Cuando haya creado un modelo útil, páselo a producción, mediante el uso de las herramientas de administración para exportarlo desde el servidor experimental a otra instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
     También puede dejar el modelo en el servidor donde lo creó, pero actualizar los datos de aprendizaje y ejecutar predicciones con Integration Services o scripts DMX.  
  
     Los usuarios avanzados apreciarán la funcionalidad **Seguimiento** , que permite ver las instrucciones DMX y XMLA enviadas al servidor.  
  
## <a name="getting-started"></a>Introducción  
 Para más información, vea [Qué se incluye en los Complementos de minería de datos para Office](http://go.microsoft.com/fwlink/p/?LinkId=616849)  
  
## <a name="support-and-requirements"></a>Compatibilidad y requisitos  
 Los Complementos de minería de datos de SQL Server para Office se descargan gratuitamente. Para usar estas herramientas, debe tener instalada una de las siguientes versiones de Office:  
  
-   Office 2010, versiones de 32 bits o de 64 bits  
  
-   Office 2013, versiones de 32 bits o de 64 bits  
  
> [!WARNING]  
>  Asegúrese de descargar la versión de los complementos que corresponda a la versión de Excel.  
  
 Los Complementos de minería de datos necesitan una conexión con una de las siguientes ediciones de SQL Server Analysis Services:  
  
-   Enterprise  
  
-   Business Intelligence  
  
-   Estándar  
  
 Dependiendo de la edición de SQL Server Analysis Services a la que se conecte, es posible que algunos algoritmos avanzados no estén disponibles. Para más información, vea [Características compatibles con las ediciones de SQL Server 2016](../../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).  
  
 Para obtener ayuda adicional con la instalación, vea esta página del centro de descarga: [http://www.microsoft.com/download/details.aspx?id=29061](http://www.microsoft.com/download/details.aspx?id=29061)  
  
  

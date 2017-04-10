---
title: "Tutorial integral de ciencia de datos | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: edd76ae9-4125-45a8-bf42-47a85b9d9a32
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# Tutorial integral de ciencia de datos
En este tutorial, desarrollará una solución de un extremo a otro para el modelado de predicción mediante [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].  
  
Este tutorial se basa en un conjunto de datos público conocido, el conjunto de datos New York City taxi. Usará una combinación de código R, datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y funciones SQL personalizadas para generar un modelo de clasificación que indique la probabilidad de que el conductor reciba una propina en un viaje de taxi determinado. También implementará el modelo R en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y usará datos del servidor para generar puntuaciones según el modelo.  
  
Este ejemplo se puede ampliar con facilidad a todos los tipos de problemas de la vida real, como predecir las respuestas de los clientes en las campañas de ventas o predecir los gastos por visitantes de eventos. Dado que el modelo se puede invocar desde un procedimiento almacenado, puede insertarlo con facilidad en una aplicación.  
  
**Público destinatario**  
  
Este tutorial está pensado para desarrolladores de R. También debe estar familiarizado con operaciones de base de datos fundamentales, como crear bases de datos, crear tablas, importar datos en tablas y consultar tablas mediante [!INCLUDE[tsql](../../includes/tsql-md.md)].  Se le proporcionarán los scripts de SQL y R que ejecutará.  
  
Si es nuevo con R pero conoce bien las bases de datos, este tutorial proporciona una introducción a cómo se puede integrar R en flujos de trabajo empresarial mediante [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. No se necesita ninguna codificación R; se proporcionan todos los scripts. Es necesario que tenga algún tipo de IDE de R instalado para ejecutar los comandos.  
  
**Requisitos previos**  
  
Para realizar este tutorial, debe tener acceso a una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] instalado. Para su entorno local, prepare una estación de trabajo de ciencia de datos que pueda conectarse a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y, después, instale las bibliotecas de R necesarias.  
  
Para obtener más información, consulte [Requisitos previos para los tutoriales de ciencia de datos &#40;SQL Server R Services&#41;](../../advanced-analytics/r-services/prerequisites-for-data-science-walkthroughs-sql-server-r-services.md).  
  
## <a name="overview"></a>Información general  
Este tutorial ilustra una solución típica de un extremo a otro para análisis avanzado. Debe completar las lecciones en orden.  
  
||Tiempo estimado para completar la lección|  
|-|------------------------------|  
|[Lección 1: Preparar los datos &#40;Tutorial integral de ciencia de datos&#41;](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)<br /><br />El proceso analítico comienza con la obtención de los datos usados para generar un modelo. Descargará un conjunto de datos público y lo guardará en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|30 minutos|  
|[Lección 2: Ver y explorar los datos &#40;Tutorial integral de ciencia de datos&#41;](../../advanced-analytics/r-services/lesson-2-view-and-explore-the-data-data-science-end-to-end-walkthrough.md)<br /><br />A menudo, un científico de datos dedica mucho tiempo a explorar los datos y prepararlos para el modelado, crear nuevas características o transformar los datos según sea necesario.  Usará tanto SQL como R para explorar los datos y generar resúmenes.|20 minutos|  
|[Lección 3: Crear características de datos &#40;Tutorial integral de ciencia de datos&#41;](../../advanced-analytics/r-services/lesson-3-create-data-features-data-science-end-to-end-walkthrough.md)<br /><br />Creará nuevas características de datos mediante las funciones personalizadas de R y [!INCLUDE[tsql](../../includes/tsql-md.md)].|10 minutos|  
|[Lección 4: Generar y guardar el modelo &#40;Tutorial integral de ciencia de datos&#41;](../../advanced-analytics/r-services/lesson-4-build-and-save-the-model-data-science-end-to-end-walkthrough.md)<br /><br />Cuando los datos estén listos, el científico de datos estudia y ajusta el modelo, evaluando su rendimiento y probando parámetros diferentes. En este tutorial, creará un modelo de clasificación y usará los datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para generar predicciones. También trazará la exactitud del modelo mediante R.|15 minutos|  
|[Lección 5: Implementar y usar el modelo &#40;Tutorial integral de ciencia de datos &#41;](../../advanced-analytics/r-services/lesson-5-deploy-and-use-the-model-data-science-end-to-end-walkthrough.md)<br /><br />Por último, implementará el modelo en producción al guardar el modelo en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y llamará al modelo desde un procedimiento almacenado para generar predicciones.|10 minutos|  
  
## <a name="notes"></a>Notas  
Dado que el tutorial está diseñado para presentar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]a los desarrolladores de R, se realiza el mayor número de acciones posible con R. Esto no significa que R sea necesariamente la mejor herramienta para cada tarea. En muchos casos, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podría proporcionar un mejor rendimiento, especialmente en tareas como la agregación de datos e ingeniería de características. Esas tareas pueden beneficiarse de las nuevas características de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], como los índices de almacén de columnas con optimización para memoria.  
  
## <a name="next-step"></a>Paso siguiente  
[Lección 1: Preparar los datos &#40;Tutorial integral de ciencia de datos&#41;](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)  
  
  
  

---
title: Preguntas más frecuentes en PolyBase | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: Abiola
ms.author: aboke
manager: ''
ms.openlocfilehash: 52fbf35d5896d602755431516c1cf93ee4949b2c
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/20/2019
ms.locfileid: "58282640"
---
# <a name="frequently-asked-questions"></a>Preguntas más frecuentes

## <a name="polybase-vs-linked-servers"></a>PolyBase frente a servidores vinculados
En la tabla siguiente se resaltan las diferencias entre las características de servidor vinculado y PolyBase:

|PolyBase | Servidores vinculados|
|--------------------------|--------------------------|  
|Objeto con ámbito de base de datos.|Objeto con ámbito de instancia.|
|Usa controladores ODBC.|Usa proveedores OLEDB.|
|Admite operaciones de solo lectura en todos los orígenes de datos y operaciones de inserción solo para HADOOP y el origen de datos del grupo de datos.|Admite tanto operaciones de lectura como de escritura.|
|Las consultas al origen de datos remotos desde una sola conexión se pueden escalar horizontalmente |Las consultas al origen de datos remotos desde una única conexión no se pueden escalar horizontalmente|
|Se admite la inserción de predicados|Se admite la inserción de predicados|
|No se necesita ninguna configuración independiente para el grupo de disponibilidad|Se necesita una configuración independiente para cada instancia del grupo de disponibilidad|
|Solo autenticación básica|Autenticación básica e integrada|
|Adecuado para procesar un gran número de filas de consultas de análisis|Adecuado para consultas OLTP que devuelven algunas filas|
|Las consultas que usan tablas externas no pueden participar en transacciones distribuidas|Las consultas distribuidas pueden participar en transacciones distribuidas|

## <a name="whats-new-in-polybase-2019"></a>Novedades en PolyBase 2019 

PolyBase en [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] puede leer ahora datos de una mayor variedad de orígenes de datos. Los datos de estos orígenes de datos externos se pueden almacenar como tablas externas en SQL Server. PolyBase además admite el cálculo de inserción en estos orígenes de datos externos, excepto los tipos de ODBC genéricos.

### <a name="compatible-data-sources"></a>Orígenes de datos compatibles

- SQL Server
- Oracle
- Teradata
- MongoDB
- Tipos genéricos de ODBC compatibles
  
> [!NOTE]
> PolyBase puede permitir la conexión a orígenes de datos externos mediante controladores ODBC de terceros. Estos controladores no se proporcionan con PolyBase y podrían no funcionar según lo previsto. Para más información, consulte la [guía](../../relational-databases/polybase/polybase-configure-odbc-generic.md) para la configuración genérica de ODBC de PolyBase.  

## <a name="polybase-in-big-data-clusters-vs-polybase-in-stand-alone-instances"></a>PolyBase en clústeres de macrodatos frente a PolyBase en instancias independientes

En la tabla siguiente se resaltan las características de PolyBase disponibles en la instalación independiente de [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] y el clúster de macrodatos de [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)]:

|Característica |Clúster de macrodatos|Instancia independiente|
|--------------------------|--------------------------|---------|   
|Crear un origen de datos externos desde SQL Server, Oracle, Teradata y Mongo DB |X|X |
|Crear un origen de datos externos con un controlador ODBC de terceros compatible | | X|
|Crear un origen de datos externos para el origen de datos HADOOP | X| X|
|Crear un origen de datos externo para Azure Blob Storage | X| X|
|Crear una tabla externa en un grupo de datos de SQL Server | X| |
|Crear una tabla externa en un grupo de almacenamiento de SQL Server | X| |
|Escalar horizontalmente la ejecución de consultas | X| X|

> [!NOTE]
>En la tabla no se describe la funcionalidad disponible en la versión más reciente de CTP de [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)]. Para ver las características disponibles, consulte las notas de la versión. Para más información sobre las conexiones mediante el conector ODBC genérico, consulte la [guía para configurar tipos genéricos de ODBC](polybase-configure-odbc-generic.md).
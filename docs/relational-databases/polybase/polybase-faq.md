---
title: Preguntas más frecuentes en PolyBase | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: Abiola
ms.author: aboke
manager: ''
ms.openlocfilehash: 331ac177831b1e07cfab253c363a35f2bab42a6c
ms.sourcegitcommit: ee76381cfb1c16e0a063315c9c7005f10e98cfe6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/26/2019
ms.locfileid: "55072887"
---
# <a name="frequently-asked-questions"></a>Preguntas más frecuentes

## <a name="polybase-in-big-data-clusters-vs-polybase-in-stand-alone-instances"></a>PolyBase en clústeres de macrodatos frente a PolyBase en instancias independientes

|Característica |Clúster de macrodatos| Instancia independiente|
|--------------------------|--------------------------|---------|   
|Crear tablas externas| X| X|
|Crear un origen de datos externos desde SQL Server, Oracle, Teradata y Mongo DB |X|X |
|Crear un origen de datos externos con un controlador ODBC de terceros compatible | | X|
|Grupos de escalabilidad horizontal de PolyBase | X | |
|Instancias de grupo de datos | X| |
|Instancias de bloque de almacenamiento| X| |

>[!NOTE]
>
>Para obtener más información sobre las conexiones mediante el conector ODBC genérico, consulte la [guía para configurar tipos genéricos de ODBC](polybase-configure-odbc-generic.md).

## <a name="whats-new-with-polybase-in-sql-server-2019"></a>Novedades de PolyBase en SQL Server 2019 

PolyBase en SQL Server 2019 ahora puede leer datos de una gama mayor de orígenes de datos. Los datos de estos orígenes de datos externos se pueden almacenar como tablas externas en SQL Server. PolyBase además admite el cálculo de inserción en estos orígenes de datos externos, excepto los tipos de ODBC genéricos. 

### <a name="compatible-data-sources"></a>Orígenes de datos compatibles

- SQL Server
- Oracle
- Teradata
- MongoDB
- Tipos genéricos de ODBC **compatibles**

  > [!NOTE]
  >
  >PolyBase puede permitir la conexión a orígenes de datos externos mediante controladores ODBC de terceros. Estos controladores no se proporcionan con PolyBase y podrían no funcionar según lo previsto. Para obtener más información, consulte la [guía](polybase-configure-odbc-generic.md) para la configuración genérica de ODBC de PolyBase.  

## <a name="polybase-vs-linked-servers"></a>PolyBase frente a servidores vinculados

|PolyBase | Servidores vinculados|
|--------------------------|--------------------------|  
|Objeto con ámbito de base de datos.|Objeto con ámbito de instancia.| 
|Usa controladores ODBC.|Usa proveedores OLEDB.| 
| Admite únicamente operaciones de solo lectura. Se va a ampliar en el futuro.| Admite únicamente operaciones de solo lectura. Se va a ampliar en el futuro.| 
|Las consultas se pueden escalar horizontalmente y se admite la inserción.|Las consultas son de un solo subproceso y se admite la inserción.|
|No se necesita ninguna configuración independiente para los grupos de disponibilidad Always On.|Se necesita una configuración independiente para cada instancia de un grupo de disponibilidad Always On.|
|Solo autenticación básica. Mejoras en SQL Server 2019|Autenticación básica e integrada|
---
title: Conectarse a orígenes de datos | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
ms.assetid: 82770486-37bd-4c90-885f-6817a7c77ad7
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 706f340ca60799cc9aa8fb745f031e1c68cc34dc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-to-data-sources"></a>Conectarse a orígenes de datos
ADO **conexión** objeto representa una sesión única con un origen de datos, incluido un DBMS, un almacén de archivos o un archivo de texto delimitado por comas. En el caso de un sistema de base de datos cliente/servidor, la conexión de ADO puede ser una conexión de red real en el servidor.  
  
 El **conexión** objeto admite varios [propiedades y métodos](../../../ado/reference/ado-api/connection-object-properties-methods-and-events.md) para especificar las configuraciones de conexión, abrir y cerrar las conexiones, crear y ejecutar comandos en el origen de datos y proporcionar información sobre el diseño del origen de datos subyacente en forma de conjuntos de filas de esquema, etcetera. Dependiendo de la funcionalidad admitida por el proveedor, algunas colecciones, métodos o propiedades de un **conexión** objeto podría no estar disponible.  
  
 Puede conectarse a un origen de datos mediante un **conexión** objeto o usando un **Recordset** objeto.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Uso de un objeto de conexión](../../../ado/guide/data/using-a-connection-object.md)  
  
-   [Mediante un objeto de conjunto de registros](../../../ado/guide/data/using-a-recordset-object.md)  
  
-   [Creación de una cadena de conexión](../../../ado/guide/data/creating-a-connection-string.md)  
  
-   [Especificar propiedades de conexión](../../../ado/guide/data/specifying-connection-properties.md)  
  
-   [Control de transacciones](../../../ado/guide/data/controlling-transactions-ado.md)

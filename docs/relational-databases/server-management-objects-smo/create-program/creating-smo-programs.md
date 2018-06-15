---
title: Crear programas SMO | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Visual Basic [SMO]
- Visual C# [SMO]
- programming [SMO]
- SQL Server Management Objects, programming
- SMO [SQL Server], programming
ms.assetid: 7d2f0bcf-f1ae-45b8-bc3f-7aea4fae7e45
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 036f5fa2b276d5cb078fdf6e9528b1877280f94e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32968130"
---
# <a name="creating-smo-programs"></a>Crear programas SMO
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  La programación general de objetos de administración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (SMO) incluye las áreas comunes que comparten todos los objetos, como ejecutar métodos, establecer propiedades y manipular colecciones.  
  
|Tema|Description|  
|-----------|-----------------|  
|[Conectarse a una instancia de SQL Server](../../../relational-databases/server-management-objects-smo/create-program/connecting-to-an-instance-of-sql-server.md)|El programa de SMO más básico que establece una conexión a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Muestra la autenticación de Windows y la autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Incluye también ejemplos que muestran cómo establecer conexión con una instancia local y una instancia remota de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[Desconectar de una instancia de SQL Server](../../../relational-databases/server-management-objects-smo/create-program/disconnecting-from-an-instance-of-sql-server.md)|Un programa que muestra cómo desconectar de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[Llamar a métodos](../../../relational-databases/server-management-objects-smo/create-program/calling-methods.md)|En esta sección se describe el enfoque general para llamar a métodos. Se muestra el uso de parámetros y cómo administrar las tablas de datos que se devuelven en un objeto <xref:System.Data.DataTable>. También incluye un ejemplo de cómo llamar a un constructor de objetos y cómo llamar a la **clon** método.|  
|[Establecer propiedades: SMO](../../../relational-databases/server-management-objects-smo/create-program/setting-properties-smo.md)|En esta sección se describe cómo establecer diferentes tipos de propiedades. Se muestra cómo establecer y obtener propiedades de objeto. También se incluyen ejemplos en los que se muestra cómo establecer propiedades de objeto cuando se crea el objeto y cómo recorrer en iteración todas las propiedades de un objeto.|  
|[Uso de colecciones](../../../relational-databases/server-management-objects-smo/create-program/using-collections.md)|Diversos programas que analizan las técnicas que se usan con colecciones de objetos. Se muestra cómo hacer referencia a un objeto utilizando colecciones. También se incluye un ejemplo de cómo recorrer en iteración los miembros de una colección.|  
|[Control de eventos SMO](../../../relational-databases/server-management-objects-smo/create-program/handling-smo-events.md)|En esta sección se describe cómo configurar y controlar eventos en SMO. Se incluye un ejemplo de cómo configurar un controlador de eventos y cómo configurar suscripciones de eventos.|  
|[Controlar excepciones SMO](../../../relational-databases/server-management-objects-smo/create-program/handling-smo-exceptions.md)|En esta sección se describe cómo detectar excepciones en SMO. Se incluyen ejemplos de cómo detectar una excepción y cómo mostrar una excepción interna.|  
|[Trabajar con tipos de datos](../../../relational-databases/server-management-objects-smo/create-program/working-with-data-types.md)|En esta sección se describe cómo trabajar con los diferentes tipos de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se describe cómo crear un tipo de datos con la especificación del constructor de objetos. También se incluye un ejemplo de cómo crear un tipo de datos utilizando el constructor predeterminado.|  
|[Uso de transacciones](../../../relational-databases/server-management-objects-smo/create-program/using-transactions.md)|En esta sección se describe cómo implementar el procesamiento de transacciones en un programa de SMO. Se incluye un ejemplo de cómo utilizar transacciones en un programa de SMO.|  
|[Usar el modo de captura](../../../relational-databases/server-management-objects-smo/create-program/using-capture-mode.md)|En esta sección se describe cómo registrar los resultados del programa de SMO. En el ejemplo se registra el programa de SMO como instrucciones [!INCLUDE[tsql](../../../includes/tsql-md.md)] enviadas a la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para su ejecución posterior.|  
  
  

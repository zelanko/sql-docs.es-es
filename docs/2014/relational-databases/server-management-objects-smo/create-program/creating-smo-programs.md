---
title: Crear programas SMO | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- Visual Basic [SMO]
- Visual C# [SMO]
- programming [SMO]
- SQL Server Management Objects, programming
- SMO [SQL Server], programming
ms.assetid: 7d2f0bcf-f1ae-45b8-bc3f-7aea4fae7e45
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ccf26cf30c53e3a336e842cbbffc1ff517075fef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68198006"
---
# <a name="creating-smo-programs"></a>Crear programas SMO
  La programación general de objetos de administración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (SMO) incluye las áreas comunes que comparten todos los objetos, como ejecutar métodos, establecer propiedades y manipular colecciones.  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Conectarse a una instancia de SQL Server](connecting-to-an-instance-of-sql-server.md)|El programa de SMO más básico que establece una conexión a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Muestra la autenticación de Windows y la autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Incluye también ejemplos que muestran cómo establecer conexión con una instancia local y una instancia remota de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[Desconectar de una instancia de SQL Server](disconnecting-from-an-instance-of-sql-server.md)|Un programa que muestra cómo desconectar de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[Llamadas a métodos](calling-methods.md)|En esta sección se describe el enfoque general para llamar a métodos. Se muestra el uso de parámetros y cómo administrar las tablas de datos que se devuelven en un objeto <xref:System.Data.DataTable>. También se incluye un ejemplo de cómo llamar a un constructor de objetos y al método `Clone`.|  
|[Establecer propiedades](setting-properties-smo.md)|En esta sección se describe cómo establecer diferentes tipos de propiedades. Se muestra cómo establecer y obtener propiedades de objeto. También se incluyen ejemplos en los que se muestra cómo establecer propiedades de objeto cuando se crea el objeto y cómo recorrer en iteración todas las propiedades de un objeto.|  
|[Usar colecciones](using-collections.md)|Diversos programas que analizan las técnicas que se usan con colecciones de objetos. Se muestra cómo hacer referencia a un objeto utilizando colecciones. También se incluye un ejemplo de cómo recorrer en iteración los miembros de una colección.|  
|[Controlar eventos SMO](handling-smo-events.md)|En esta sección se describe cómo configurar y controlar eventos en SMO. Se incluye un ejemplo de cómo configurar un controlador de eventos y cómo configurar suscripciones de eventos.|  
|[Controlar excepciones SMO](handling-smo-exceptions.md)|En esta sección se describe cómo detectar excepciones en SMO. Se incluyen ejemplos de cómo detectar una excepción y cómo mostrar una excepción interna.|  
|[Trabajar con tipos de datos](working-with-data-types.md)|En esta sección se describe cómo trabajar con los diferentes tipos de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se describe cómo crear un tipo de datos con la especificación del constructor de objetos. También se incluye un ejemplo de cómo crear un tipo de datos utilizando el constructor predeterminado.|  
|[Utilizar transacciones](using-transactions.md)|En esta sección se describe cómo implementar el procesamiento de transacciones en un programa de SMO. Se incluye un ejemplo de cómo utilizar transacciones en un programa de SMO.|  
|[Utilizar el modo de captura](using-capture-mode.md)|En esta sección se describe cómo registrar los resultados del programa de SMO. En el ejemplo se registra el programa de SMO como instrucciones [!INCLUDE[tsql](../../../includes/tsql-md.md)] enviadas a la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para su ejecución posterior.|  
  
  

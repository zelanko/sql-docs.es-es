---
title: Ejecutar lógica de negocios durante la sincronización de mezcla | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- custom error resolution [SQL Server replication]
- custom change handling [SQL Server replication]
- errors [SQL Server replication], business logic handlers
- merge replication business logic handlers [SQL Server replication]
- conflict resolution [SQL Server replication], merge replication
- business logic handlers [SQL Server replication]
ms.assetid: 9d4da2ef-c17f-4a31-a1f6-5c3b7ca85f71
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 440419f1fb4670ff5bdfc2e49cd9cfe6fa5df65e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/25/2020
ms.locfileid: "62999565"
---
# <a name="execute-business-logic-during-merge-synchronization"></a>Ejecutar lógica de negocios durante la sincronización de mezcla
  El marco de trabajo de controladores de lógica de negocios permite escribir un ensamblado de código administrado al que se llama durante el proceso de sincronización de mezcla. El ensamblado incluye lógica de negocios que puede responder a varias condiciones durante la sincronización: cambios de datos, conflictos y errores. El marco de trabajo de controladores de lógica de negocios proporciona un modelo de programación simple y los datos que el proceso de mezcla suministra al ensamblado tienen el formato de un conjunto de datos ADO.NET, lo que permite aprovechar el conocimiento de ADO.NET en lugar de aprender el uso de una interfaz privada. Para obtener más información acerca de los controladores de lógica de negocios de programación, vea:  
  
-   Referencia de la interfaz de programación de aplicaciones (API): <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>  
  
-   Instrucciones sobre cómo implementar un controlador de lógica de negocios: [Implement a Business Logic Handler for a Merge Article](../implement-a-business-logic-handler-for-a-merge-article.md) (Implementar un controlador de lógica de negocios para un artículo de mezcla)  
  
## <a name="uses-for-business-logic-handlers"></a>Usos de los controladores de lógica de negocios  
 El proceso de sincronización de mezcla puede invocar controladores de lógica de negocios para que lleven a cabo las siguientes acciones:  
  
-   Control personalizado de cambios  
  
-   Resolución personalizada de conflictos  
  
-   Resolución personalizada de errores  
  
> [!NOTE]  
>  El controlador de lógica de negocios especificado se ejecuta para cada fila que se sincroniza. La lógica compleja y las llamadas a otras aplicaciones o servicios de red pueden afectar al rendimiento.  
  
### <a name="custom-change-handling"></a>Control personalizado de cambios  
 Se puede invocar el controlador de lógica de negocios durante el procesamiento de cambios de datos que no produzcan conflictos y realizar una de estas tres acciones:  
  
-   Rechazar los datos  
  
     Esto resulta útil para aplicaciones que no desean propagar los datos a un suscriptor o de un suscriptor determinado. Por ejemplo, un administrador puede filtrar las inserciones que no pertenezcan a la partición del suscriptor, o bien rechazar las eliminaciones realizadas en un suscriptor. O bien, una aplicación podría rechazar un pedido realizado en un suscriptor debido a que el inventario ya no está disponible.  
  
-   Aceptar los datos  
  
     Esto es útil para aplicaciones en las que es necesario revisar los cambios de datos realizados en el publicador o en el suscriptor antes de permitir que se propaguen. Por ejemplo, una aplicación de nivel intermedio podría examinar los pedidos de campo nuevos e integrarlos con un proceso de flujo de trabajo de compras en dicho nivel.  
  
-   Aplicar datos personalizados  
  
     Esto es útil para aplicaciones que deben suplantar operaciones o valores de datos específicos. Por ejemplo, una aplicación podría transformar la eliminación de una fila en una actualización especial que establezca la columna **estado** de la fila en el valor "eliminado" y después realice un seguimiento de la identidad del cliente que lleva a cabo la eliminación. Esto podría ser útil con fines de auditoría o flujo de trabajo.  
  
### <a name="custom-conflict-resolution"></a>Resolución personalizada de conflictos  
 La replicación de mezcla permite la detección y resolución de conflictos, y permite al usuario aceptar una estrategia de resolución predeterminada o elegir la resolución personalizada de los conflictos. Para obtener más información, vea [detección y resolución de conflictos de replicación de mezcla avanzada](advanced-merge-replication-conflict-detection-and-resolution.md). Se puede invocar el controlador de lógica de negocios durante el procesamiento de cambios de datos que produzcan conflictos y realizar una de estas dos acciones:  
  
-   Aceptar la resolución predeterminada  
  
     Esto es útil para aplicaciones que pueden necesitar revisar el conflicto, realizar otras acciones y, posiblemente, registrar un mensaje de conflicto personalizado.  
  
-   Realizar una resolución personalizada  
  
     Esto es útil para aplicaciones que pueden necesitar seleccionar valores de datos específicos para su lógica de negocios y suministrar este conjunto de datos personalizado al proceso de sincronización. Por ejemplo, una aplicación podría proporcionar una nueva versión de la fila ganadora combinando valores de los conjuntos de datos del publicador y el suscriptor.  
  
### <a name="custom-error-resolution"></a>Resolución personalizada de errores  
 Se puede invocar la lógica personalizada durante la propagación de cambios que dan como resultado errores. La lógica puede realizar una de las dos acciones siguientes:  
  
-   Aceptar la resolución predeterminada del error  
  
     Esto es útil para aplicaciones que pueden necesitar revisar el error, realizar otras acciones y, posiblemente, registrar un mensaje de error personalizado.  
  
-   Aceptar la resolución personalizada del error  
  
     Esto es útil para aplicaciones que pueden necesitar seleccionar valores de datos específicos para su lógica de negocios y suministrar este conjunto de datos personalizado al proceso de sincronización. Por ejemplo, si el proceso de replicación detecta una infracción de clave duplicada, el controlador de lógica de negocios podría proporcionar una nueva versión del cambio de datos en la que la clave ya no entre en conflicto. Después, los cambios realizados en el publicador y el suscriptor pueden persistir en la base de datos y el proceso de replicación no tiene que compensar el error de inserción con una eliminación.  
  
## <a name="deployment-scenarios-for-business-logic-handlers"></a>Escenarios de implementación de controladores de lógica de negocios  
 Los controladores de lógica de negocios se pueden implementar en:  
  
-   El distribuidor. Utilice una suscripción de inserción para que la lógica de negocios se ejecute en el distribuidor.  
  
-   El suscriptor. Utilice una suscripción de extracción para que la lógica de negocios se ejecute en el suscriptor.  
  
-   Un servidor con Internet Information Services (IIS), si se utiliza la sincronización web. Utilice una suscripción de extracción sincronizada con la sincronización web y el controlador de lógica de negocios se ejecutará en el servidor IIS.  
  
## <a name="see-also"></a>Consulte también  
 [Replicación de mezcla](merge-replication.md)   
 [Subscribe to Publications](../subscribe-to-publications.md)   
 [Sincronizar datos](../synchronize-data.md)   
 [Sincronización web para la replicación de mezcla](../web-synchronization-for-merge-replication.md)  
  
  

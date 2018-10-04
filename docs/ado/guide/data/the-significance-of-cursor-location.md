---
title: La importancia de la ubicación del Cursor | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- server-side cursors [ADO]
- cursors [ADO], client-side
- client-side cursors [ADO]
- cursors [ADO], server-side
ms.assetid: 70ef5b1c-0459-41a1-b796-031f61a29a8a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d25153a3c84340ad6feea43aa969ef52d358fe4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47717723"
---
# <a name="the-significance-of-cursor-location"></a>La importancia de la ubicación del Cursor
Cada cursor utiliza recursos temporales para almacenar sus datos. Estos recursos pueden ser un archivo de paginación de disco, memoria, los archivos de disco temporal o incluso almacenamiento temporal en la base de datos. El cursor se denomina un *del lado cliente* cursor cuando estos recursos están ubicados en el equipo cliente. El cursor se denomina un *servidor* cursor cuando estos recursos están ubicados en el servidor.  
  
## <a name="client-side-cursors"></a>Cursores del lado cliente  
 En ADO, llamar para un cursor de cliente mediante el **adUseClient CursorLocationEnum.** Con un cursor de cliente sin conjunto de claves, el servidor envía el resultado completo a través de la red en el equipo cliente. El equipo cliente proporciona y administra los recursos temporales necesarios para el cursor y conjunto de resultados. La aplicación cliente puede examinar el resultado completo para determinar qué filas requiere.  
  
 Estáticos y controlado por los cursores del lado cliente pueden colocar una carga significativa en la estación de trabajo si incluyen demasiadas filas. Mientras que todas las bibliotecas de cursor son capaces de crear cursores con miles de filas, las aplicaciones diseñadas para capturar estos grandes conjuntos de filas es posible que un rendimiento deficiente. Hay excepciones, por supuesto. Para algunas aplicaciones, un cursor de cliente grande podría ser perfectamente adecuado y el rendimiento podría no ser un problema.  
  
 Una ventaja obvia del cursor del lado cliente es una respuesta rápida. Después de que el conjunto de resultados se ha descargado en el equipo cliente, examine las filas es muy rápida. La aplicación es generalmente más escalable con cursores de cliente porque los requisitos de recursos del cursor se colocan en cada cliente por separado y no en el servidor.  
  
## <a name="server-side-cursors"></a>Cursores de servidor  
 En ADO, llamar a un cursor de servidor por utilizando el **adUseServer CursorLocationEnum.** Con un cursor de servidor, el servidor administra el conjunto de resultados mediante recursos proporcionados por el equipo del servidor. El cursor de servidor devuelve solo los datos solicitados a través de la red. Este tipo de cursor a veces puede proporcionar un mejor rendimiento que el cursor del lado cliente, especialmente en situaciones donde el tráfico de red excesiva es un problema.  
  
 Sin embargo, es importante señalar que es un cursor de servidor, por lo menos temporalmente, consumen valiosos recursos del servidor para cada cliente activo. Debe planear en consecuencia para asegurarse de que el hardware del servidor es capaz de administrar todos los cursores de servidor solicitados por los clientes activos. Además, un cursor de servidor puede ser lento porque proporciona acceso de fila única solo: no hay disponible ningún cursor de batch.  
  
 Cursores de servidor son útiles al insertar, actualizar o eliminar registros. Con cursores de servidor, puede tener varias instrucciones activas en la misma conexión.

---
title: La importancia de la ubicación del Cursor | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- server-side cursors [ADO]
- cursors [ADO], client-side
- client-side cursors [ADO]
- cursors [ADO], server-side
ms.assetid: 70ef5b1c-0459-41a1-b796-031f61a29a8a
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5699c8c7bc3ab1ed54d9411ff889e43e8cf334d5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="the-significance-of-cursor-location"></a>La importancia de la ubicación del Cursor
Cada cursor utiliza recursos temporales para almacenar sus datos. Estos recursos pueden ser memoria, un archivo de paginación de disco, archivos de disco temporal o incluso almacenamiento temporal en la base de datos. El cursor se denomina un *cliente* cursor cuando estos recursos están ubicados en el equipo cliente. El cursor se denomina un *servidor* cursor cuando estos recursos están ubicados en el servidor.  
  
## <a name="client-side-cursors"></a>Cursores del lado cliente  
 En ADO, llamar para un cursor de cliente mediante el **adUseClient CursorLocationEnum.** Con un cursor de cliente sin conjunto de claves, el servidor envía el resultado completo a través de la red en el equipo cliente. El equipo cliente proporciona y administra los recursos temporales que necesita el cursor y conjunto de resultados. La aplicación de cliente puede examinar el resultado completo para determinar qué filas requiere.  
  
 Cursores estáticos y controlados por conjunto de claves del lado cliente pueden suponer una carga importante en la estación de trabajo si incluyen demasiadas filas. Aunque todas las bibliotecas de cursor de son capaces de crear cursores con miles de filas, las aplicaciones diseñadas para capturar estos conjuntos de filas grandes pueden mediocre. Por supuesto, hay excepciones. En algunas aplicaciones, un cursor de cliente grande podría ser perfectamente apropiado y no podría ser un problema de rendimiento.  
  
 Una ventaja obvia del cursor de cliente es una respuesta rápida. Después de que el conjunto de resultados se ha descargado en el equipo cliente, examine las filas es muy rápida. La aplicación es generalmente más escalable con cursores de cliente porque los requisitos de recursos del cursor se colocan en cada cliente por separado y no en el servidor.  
  
## <a name="server-side-cursors"></a>Cursores de servidor  
 En ADO, llamar a un cursor de servidor por mediante el **adUseServer CursorLocationEnum.** Con un cursor de servidor, el servidor administra el conjunto de resultados mediante recursos proporcionados por el equipo del servidor. El cursor de servidor devuelve sólo los datos solicitados a través de la red. Este tipo de cursor a veces puede proporcionar un mejor rendimiento que el cursor del lado cliente, sobre todo en situaciones donde excesivo tráfico de red es un problema.  
  
 Sin embargo, es importante señalar que es un cursor de servidor, por lo menos temporalmente: consumir valiosos recursos del servidor para cada cliente activo. Debe planear en consecuencia para asegurarse de que el hardware del servidor es capaz de administrar todos los cursores de servidor solicitados por clientes activos. Además, un cursor de servidor puede ser lento porque proporciona solo acceso a una fila, no hay ningún cursor lote disponible.  
  
 Cursores de servidor son útiles al insertar, actualizar o eliminar registros. Con cursores de servidor, puede tener varias instrucciones activas en la misma conexión.

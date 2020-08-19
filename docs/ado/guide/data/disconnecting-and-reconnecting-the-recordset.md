---
description: Desconectar y volver a conectar el conjunto de registros
title: Desconectar y volver a conectar el conjunto de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset object [ADO], disconnecting and reconnecting
ms.assetid: c5134af7-81d6-4de4-9fd1-cfe29973545e
author: rothja
ms.author: jroth
ms.openlocfilehash: f372951375954a4ed93213cc7cbfd7bc99ef1ecf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453487"
---
# <a name="disconnecting-and-reconnecting-the-recordset"></a>Desconectar y volver a conectar el conjunto de registros
Una de las características más eficaces que se encuentran en ADO es la capacidad de abrir un conjunto de registros del lado cliente desde un origen de datos y, a continuación, desconectar el conjunto de registros del origen de datos. Una vez que se ha desconectado el conjunto de registros, se puede cerrar la conexión al origen de datos, con lo que se liberan los recursos del servidor que se usan para mantenerlo. Puede seguir viendo y editando los datos en el conjunto de registros mientras está desconectado y, posteriormente, volver a conectarse al origen de datos y enviar las actualizaciones en modo por lotes.  
  
 Para desconectar un conjunto de registros, ábralo con una ubicación de cursor de adUseClient y, a continuación, establezca el valor de la propiedad ActiveConnection en Nothing. (Los usuarios de C++ deben establecer el valor de ActiveConnection en NULL para desconectar).  
  
 Usaremos un conjunto de registros desconectado más adelante en esta sección cuando se analice la persistencia del conjunto de registros para abordar un escenario en el que es necesario que los datos de un conjunto de registros estén disponibles para una aplicación mientras el equipo cliente no está conectado a una red.  
  
## <a name="see-also"></a>Consulte también  
 [Batch Mode](../../../ado/guide/data/batch-mode.md)

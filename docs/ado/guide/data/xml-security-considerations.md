---
description: Consideraciones de seguridad XML
title: Consideraciones sobre seguridad de XML | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML security in ADO
ms.assetid: fadbd38e-6e7b-4b81-96ea-85169c664374
author: rothja
ms.author: jroth
ms.openlocfilehash: 608ad67d531573d0124ea312252e6d30c289bf15
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978796"
---
# <a name="xml-security-considerations"></a>Consideraciones de seguridad XML
Los métodos Save y Open de ADO en el objeto de conjunto de registros no se consideran operaciones seguras para ejecutarse en Internet Explorer. Por lo tanto, si se usan estos métodos en un código de script que se ejecuta en una aplicación o un control que se hospeda en un explorador, la configuración de seguridad del explorador afectará a su comportamiento.  
  
 Internet Explorer 5 proporciona restricciones de seguridad para dichas operaciones de forma predeterminada en las zonas de Internet. En esa configuración, el conjunto de registros no puede tener acceso al sistema de archivos local en el cliente ni tener acceso a ningún origen de datos fuera del dominio del servidor desde el que se ha descargado la página. En concreto, cuando se ejecuta dentro del host del explorador, un conjunto de registros se puede guardar en un archivo solo si se encuentra en el mismo servidor desde el que se descargó la página. Del mismo modo, puede abrir un conjunto de registros si lo carga desde un archivo sólo si ese archivo está en el mismo servidor desde el que se descargó la página.  
  
## <a name="see-also"></a>Consulte también  
 [Almacenar registros en formato XML](./persisting-records-in-xml-format.md)
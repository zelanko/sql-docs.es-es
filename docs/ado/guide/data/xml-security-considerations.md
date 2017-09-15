---
title: Consideraciones de seguridad XML | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML security in ADO
ms.assetid: fadbd38e-6e7b-4b81-96ea-85169c664374
caps.latest.revision: 3
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fc94f80cde09f6ad55de3a108b6fd16ef74444f1
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="xml-security-considerations"></a>Consideraciones de seguridad XML
Los métodos abiertos en el objeto de conjunto de registros y Save de ADO no se consideran operaciones seguras para ejecutarse en Internet Explorer. Por lo tanto, si estos métodos se usan en un código de script que se ejecuta en una aplicación o control que se hospeda en un explorador, la configuración de seguridad del explorador tendrá un efecto en su comportamiento.  
  
 Internet Explorer 5 proporciona restricciones de seguridad para operaciones de forma predeterminada en las zonas de Internet. En esa configuración, el conjunto de registros no puede obtener acceso al sistema de archivos local en el cliente ni tener acceso a los orígenes de datos fuera del dominio del servidor desde el que se ha descargado la página. En concreto, cuando se ejecuta en el host del explorador, un conjunto de registros puede guardarse en un archivo solo si está en el mismo servidor desde el que se descargó la página. De forma similar, puede abrir un conjunto de registros mediante la carga de un archivo sólo si ese archivo está en el mismo servidor desde el que se descargó la página.  
  
## <a name="see-also"></a>Vea también  
 [Almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)

---
title: Consideraciones de seguridad XML | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML security in ADO
ms.assetid: fadbd38e-6e7b-4b81-96ea-85169c664374
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fa0e9e2df1e8ba3f44b10e662d25e536ac7962f8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923354"
---
# <a name="xml-security-considerations"></a>Consideraciones de seguridad XML
Los métodos abiertos en el objeto de conjunto de registros y guardar ADO no se consideran operaciones seguras para ejecutarse en Internet Explorer. Por lo tanto, si estos métodos se usan en un código de script que se ejecuta en una aplicación o control que se hospeda en un explorador, la configuración de seguridad del explorador tendrá un efecto en su comportamiento.  
  
 Internet Explorer 5 proporciona restricciones de seguridad para operaciones de forma predeterminada en las zonas de Internet. En esa configuración, el conjunto de registros no se puede obtener acceso al sistema de archivos local en el cliente o tener acceso a los orígenes de datos fuera del dominio del servidor desde el que se ha descargado la página. En concreto, cuando se ejecuta en el host del explorador, un conjunto de registros puede guardarse en un archivo solo si se encuentra en el mismo servidor desde el que se descargó la página. De forma similar, puede abrir un conjunto de registros cargándola desde un archivo sólo si ese archivo está en el mismo servidor desde el que se descargó la página.  
  
## <a name="see-also"></a>Vea también  
 [Almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)

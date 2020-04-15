---
title: Recuperación de los valores en los campos descriptores de la página de valores de la empresa de valores de la página de valores de Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: c05b180f-c2b0-437b-8d1c-ce7f4da93287
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 43467d19f3f2e576efa0402c4ba513e23da59390
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304326"
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>Recuperar los valores de campos de Descriptor
Una aplicación puede llamar a **SQLGetDescField** para obtener un único campo de un registro descriptor. **SQLGetDescField** proporciona a la aplicación acceso a todos los campos descriptores definidos en ODBC y a los campos definidos por el controlador también.  
  
 **SQLGetDescRec** se puede llamar para recuperar la configuración de varios campos descriptores que afectan al tipo de datos y el almacenamiento de datos de columna o parámetro.

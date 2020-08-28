---
description: Capturar códigos de error de ADO
title: Códigos de error de ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO], error codes
ms.assetid: 3aee61c7-a9b7-4596-b78e-5828a00d0281
author: rothja
ms.author: jroth
ms.openlocfilehash: aa933f7be33f564af3aaf2851f6ec32bd5b4c5d4
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991194"
---
# <a name="capture-ado-error-codes"></a>Capturar códigos de error de ADO
Además de los errores de proveedor devueltos en los objetos de [error](../../reference/ado-api/error-object.md) de la colección de [errores](../../reference/ado-api/errors-collection-ado.md) , ADO puede devolver errores al mecanismo de control de excepciones del entorno en tiempo de ejecución. Use el mecanismo de captura de errores del lenguaje de programación, como la instrucción **on error** de Microsoft® Visual Basic, o el bloque **try-catch** de Microsoft Visual C++® para capturar errores de ADO.

 Para obtener la lista de códigos de error de ADO, vea [ErrorValueEnum](../../reference/ado-api/errorvalueenum.md).

## <a name="see-also"></a>Consulte también
 Colección de errores de [objetos de error](../../reference/ado-api/error-object.md) [(ADO)](../../reference/ado-api/errors-collection-ado.md)
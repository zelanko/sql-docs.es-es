---
title: Modo de confirmación automática (Auto-Commit Mode) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- auto-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: c8de5b60-d147-492d-b601-2eeae8511d00
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6f19053eec7a48eba7a51425b01744f3acd10015
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285115"
---
# <a name="auto-commit-mode"></a>Modo de confirmación automática
*En el modo de confirmación automática,* cada operación de base de datos es una transacción que se confirma cuando se realiza. Este modo es adecuado para muchas transacciones del mundo real que constan de una sola instrucción SQL. No es necesario delimitar o especificar la finalización de estas transacciones. En las bases de datos sin compatibilidad con transacciones, el modo de confirmación automática es el único modo admitido. En estas bases de datos, las instrucciones se confirman cuando se ejecutan y no hay forma de revertirlas; por lo tanto, siempre están en modo de confirmación automática.  
  
 Si el DBMS subyacente no admite transacciones de modo de confirmación automática, el controlador puede emularlas confirmando manualmente cada instrucción SQL a medida que se ejecuta.  
  
 Si un lote de instrucciones SQL se ejecuta en modo de confirmación automática, es específico del origen de datos cuando se confirman las instrucciones del lote. Se pueden confirmar tal como se ejecutan o como un todo después de que se haya ejecutado todo el lote. Algunas fuentes de datos pueden admitir ambos comportamientos y pueden proporcionar una manera de seleccionar uno o los otros. En particular, si se produce un error en medio del lote, es específico del origen de datos si las instrucciones ya ejecutadas se confirman o se revierten. Por lo tanto, las aplicaciones interoperables que utilizan lotes y requieren que se confirmen o reviertan en su conjunto deben ejecutar lotes solo en modo de confirmación manual.

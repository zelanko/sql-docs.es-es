---
title: Modo de confirmación automática | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a8a02d58309f123e6cc8b29d41188ba5bebb26f7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67909889"
---
# <a name="auto-commit-mode"></a>Modo de confirmación automática
*En el modo de confirmación automática,* cada operación de base de datos es una transacción que se confirma cuando se realiza. Este modo es adecuado para muchas transacciones del mundo real que se componen de una única instrucción SQL. No es necesario delimitar o especificar la finalización de estas transacciones. En las bases de datos sin compatibilidad con transacciones, el modo de confirmación automática es el único que se admite. En esas bases de datos, las instrucciones se confirman cuando se ejecutan y no hay ninguna manera de revertirlos. por lo tanto, están siempre en modo de confirmación automática.  
  
 Si el DBMS subyacente no es compatible con las transacciones del modo de confirmación automática, el controlador puede emularlas mediante la confirmación manual de cada instrucción SQL a medida que se ejecuta.  
  
 Si un lote de instrucciones SQL se ejecuta en modo de confirmación automática, es específico del origen de datos cuando se confirman las instrucciones del lote. Se pueden confirmar a medida que se ejecutan o en su totalidad una vez que se ha ejecutado todo el lote. Algunos orígenes de datos pueden admitir ambos comportamientos y pueden proporcionar una manera de seleccionar uno o los demás. En concreto, si se produce un error en medio del lote, es específico del origen de datos si se confirman o se revierten las instrucciones que ya se han ejecutado. Por lo tanto, las aplicaciones interoperables que usan lotes y requieren que se confirmen o reviertan en su totalidad deben ejecutar lotes solo en el modo de confirmación manual.

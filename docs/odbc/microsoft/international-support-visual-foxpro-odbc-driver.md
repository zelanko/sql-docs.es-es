---
title: Soporte internacional (controlador ODBC de Visual FoxPro) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- double-byte character sets [ODBC]
- FoxPro ODBC driver [ODBC], international support
- DBCS [ODBC]
- international support [ODBC]
- sort order [ODBC]
- collating sequences [ODBC]
- Visual FoxPro ODBC driver [ODBC], international support
ms.assetid: cd3fab32-13f1-4a86-abc4-5e18667669fc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b4b0c758bb478ea6a468e6756c3d6f0f52c766f5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299975"
---
# <a name="international-support-visual-foxpro-odbc-driver"></a>Compatibilidad internacional (controlador ODBC de Visual FoxPro)
El controlador ODBC de Microsoft Visual FoxPro admite:  
  
-   Conjuntos de caracteres de doble byte (DBCS)  
  
-   Múltiples secuencias de intercalación  
  
 Una secuencia de intercalación define el criterio de *ordenación* de los datos almacenados en una tabla o base de datos de Visual FoxPro. De forma predeterminada, el controlador está configurado para usar las secuencias de intercalación que admiten la versión de idioma del sistema operativo.  
  
 Para obtener una lista de las secuencias de intercalación admitidas, consulte [SET COLLATE](../../odbc/microsoft/set-collate-command.md).  
  
## <a name="locale"></a>locale  
 El conjunto de información que corresponde a un idioma y un país o región determinados. Una configuración regional indica valores específicos, como separadores decimales, formatos de fecha y hora y orden de caracteres.  
  
## <a name="sort-order"></a>criterio de ordenación  
 Los pedidos de ordenación incorporan las reglas de ordenación de diferentes *configuraciones regionales,* lo que le permite ordenar los datos en esos idiomas correctamente. En Visual FoxPro, el criterio de ordenación actual determina los resultados de las comparaciones de expresiones de caracteres y el orden en que aparecen los registros en tablas indizadas o ordenadas.

---
title: Tipos de cursor | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC applications, cursors
- cursors [ODBC], types
- ODBC cursors, types
ms.assetid: 3a916cc7-f352-42cb-8b83-f78e06cef991
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a5b073ee58c0e29b1d7e6d02d079141838cef237
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705675"
---
# <a name="cursor-types"></a>Tipos de cursor
  ODBC define cuatro tipos de cursor compatibles con Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client. Estos cursores varían en función de la capacidad de detectar cambios en el conjunto de resultados y en los recursos que consumen, como la memoria y el espacio en **tempdb**. Un cursor solamente puede detectar cambios en las filas cuando intenta volver a capturar estas filas; el origen de datos no dispone de ningún método para notificar al cursor los cambios en las filas actualmente capturadas. El nivel de aislamiento de transacción también afecta la capacidad de un cursor para detectar modificaciones que no se realizaron a través del cursor.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite cuatro tipos de cursor ODBC:  
  
-   Los cursores de solo avance no admiten el desplazamiento; solo admiten la captura de filas en serie desde el inicio hasta el final del cursor.  
  
-   Los cursores estáticos se crean en **tempdb** cuando se abre el cursor. Siempre muestran el conjunto de resultados tal como estaba al abrir el cursor. Nunca reflejan los cambios en los datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursores estáticos son siempre de solo lectura. Dado que un cursor de servidor estático se genera como una tabla de trabajo en **tempdb**, el tamaño del conjunto de resultados del cursor no puede superar el tamaño de fila máximo permitido por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   En los cursores controlados por conjunto de claves, la pertenencia y el orden de las filas del conjunto de resultados se fijan al abrir el cursor. Los cambios en las columnas sin clave son visibles a través del cursor.  
  
-   Los cursores dinámicos son los opuestos a los cursores estáticos. Reflejan todas las modificaciones realizadas en las filas de su conjunto de resultados. Los valores de datos, el orden y la pertenencia de las filas del conjunto de resultados pueden cambiar con cada captura.  
  
## <a name="see-also"></a>Consulte también  
 [Usar cursores &#40;&#41;ODBC](using-cursors-odbc.md)  
  
  

---
title: PDO::rollback | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d918c1e3-1be0-4001-b3b0-000db6d9e8b8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0f0d3760be13b157f7e711539c0be88bd9856d1d
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80919049"
---
# <a name="pdorollback"></a>PDO::rollback
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Descarta los comandos de base de datos que se ejecutaron después de llamar a [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) y devuelve la conexión al modo de confirmación automática.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
bool PDO::rollBack ();  
```  
  
## <a name="return-value"></a>Valor devuelto  
Se devuelve el valor True si la llamada al método se realizó correctamente; en caso contrario, se devuelve False.  
  
## <a name="remarks"></a>Observaciones  
El valor de PDO::ATTR_AUTOCOMMIT no afecta a PDO::rollback.  
  
Consulte [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) para ver un ejemplo donde se utiliza PDO::rollback.  
  
En la versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], se agregó compatibilidad con PDO.  
  
## <a name="see-also"></a>Consulte también  
[Clase PDO](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  

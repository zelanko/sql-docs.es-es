---
title: PDO::getAvailableDrivers | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: eab561e6-1229-401a-9482-008c23f9a4e6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0a9b24f4f8d0481ebf127a1619968b2c88c9e1d0
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80919287"
---
# <a name="pdogetavailabledrivers"></a>PDO::getAvailableDrivers
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Devuelve una matriz de los controladores de PDO en la instalación de PHP.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
array PDO::getAvailableDrivers ();  
```  
  
## <a name="return-value"></a>Valor devuelto  
Una matriz con la lista de controladores de PDO.  
  
## <a name="remarks"></a>Observaciones  
El nombre del controlador de PDO se utiliza en PDO::__construct para crear una instancia de PDO.  
  
No se requiere implementar PDO::getAvailableDrivers mediante los controladores PHP. Para obtener más información sobre este método, consulte la documentación de PHP.  
  
En la versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], se agregó compatibilidad con PDO.  
  
## <a name="example"></a>Ejemplo  
  
```  
<?php  
print_r(PDO::getAvailableDrivers());  
?>  
```  
  
## <a name="see-also"></a>Consulte también  
[Clase PDO](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  

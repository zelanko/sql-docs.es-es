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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 52df84278079a9d1c7f7e7c23e4c86b5413758e9
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66762203"
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
  
## <a name="remarks"></a>Notas  
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
  

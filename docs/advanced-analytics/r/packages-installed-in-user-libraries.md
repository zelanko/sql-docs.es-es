---
title: Paquetes instalados en bibliotecas de usuario | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 99ffd9b8-aa6d-4ac2-9840-4e66d0463978
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b4d5c7f3d1d0da5e1967140fcbdfcf60ba4571e7
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="packages-installed-in-user-libraries"></a>Paquetes instalados en bibliotecas de usuario

Si un usuario necesita un nuevo paquete de R y no es un administrador, los paquetes no se pueden instalar en la ubicación predeterminada, sino que se instalan de forma predeterminada en una biblioteca de usuario privada. 

En un entorno de desarrollo de R al uso, para hacer referencia al paquete en el código, el usuario tendría que agregar la ubicación a la variable de entorno de R `libPath`, o bien hacer referencia a la ruta de acceso completa del paquete, como aquí:  
  
~~~~
library("c:/Users/<username>/R/win-library/packagename")  
~~~~

## <a name="problems-with-packages-in-user-libraries"></a>Problemas con los paquetes en bibliotecas de usuario

A pesar de lo anterior, en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] esta solución **no** es viable: los paquetes se deben instalar en la biblioteca predeterminada. Si el paquete no está instalado en la biblioteca predeterminada, podría aparecer este error al intentar llamar al paquete:

*Error in library(xxx): there is no package called 'xxx'* (Error en la biblioteca (xxx): no hay ningún paquete llamado 'xxx')
 

Por lo tanto, al migrar soluciones de R para ejecutarse en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], es importante que haga lo siguiente:
+ Instalar los paquetes que necesite en la biblioteca predeterminada.
+ Editar el código para asegurarse de que los paquetes se cargan desde la biblioteca predeterminada, y no desde directorios ad hoc o desde bibliotecas de usuario.
+ Comprobar el código para asegurarse de que no hay ninguna llamada a paquetes no instalados.
+ Modificar cualquier código que intente instalar paquetes de forma dinámica.
 
Si un paquete está instalado en la biblioteca predeterminada, el tiempo de ejecución de R lo cargará desde la biblioteca predeterminada, aunque se haya especificado otra biblioteca en el código de R.

## <a name="see-also"></a>Vea también

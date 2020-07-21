---
title: Configuración regional ajena a la del sistema | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- locale, linux, macOS, system
author: yitam
ms.author: v-yitam
manager: v-mabarw
ms.openlocfilehash: bd60bff3ab9ee19b1a1d2435e69651ea054689e7
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "76913328"
---
# <a name="non-system-locale-settings"></a>Configuración regional ajena a la del sistema
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Esta sección solo se aplica a los usuarios de Linux y macOS, en concreto aquellos que se ocupan de más de una configuración regional en sus aplicaciones PHP.

De forma predeterminada, [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] toma la variable de entorno `LC_ALL` definida en el sistema e invalida todas las demás categorías de `LC_xxx` (con la excepción quizás de `$LANG` o `$LANGUAGE` en algunas circunstancias), lo que afecta el separador de miles, el carácter de separador decimal, el juego de caracteres, el mes, los nombres de los días, los mensajes de aplicación como los mensajes de error, el símbolo de moneda, etc.

A partir de la versión 5.8.0, los usuarios pueden configurar los valores de localización mediante el archivo php.ini, tal como se muestra en los ejemplos siguientes.

## <a name="set-locale-info-using-the-sqlsrv-driver"></a>Establecimiento de la información de configuración regional mediante el controlador SQLSRV  
Agregue lo siguiente al final del archivo php.ini:
  
```  
[sqlsrv]  
sqlsrv.SetLocaleInfo = <option>
```  
  
## <a name="set-locale-info-using-the-pdo_sqlsrv-driver"></a>Establecimiento de la información de configuración regional mediante el controlador PDO_SQLSRV  
Agregue lo siguiente al final del archivo php.ini:
  
```  
[pdo_sqlsrv]  
pdo_sqlsrv.set_locale_info = <option>
```  
  
La **opción** puede ser uno de los valores siguientes:  
  
|Opción|Descripción del comportamiento|
|---------|---------------|
|0|El controlador omite la configuración regional del sistema.|
|1|El controlador lee la variable LC_CTYPE.|
|2|El controlador lee la variable LC_ALL (este es el valor predeterminado).|
  

La categoría `LC_CTYPE` determina las reglas de control de caracteres, que son las que rigen la interpretación de secuencias de bytes de los caracteres de datos de texto, la clasificación de caracteres y el comportamiento de las clases de caracteres. Controla el reconocimiento de caracteres en mayúsculas y minúsculas, alfabéticos y no alfabéticos, etc.

### <a name="explanation"></a>Explicación

1. Opción 0: úsela si no desea modificar la configuración regional de la aplicación.

1. Opción 1: úsela para establecer solo el valor del sistema de `LC_CTYPE` sin que afecte a las demás categorías de `LC_xxx`.

1. Option 2 : use `LC_ALL` para invalidar todas las categorías de `LC_xxx`, lo que afecta la aplicación PHP y sus extensiones.

Si la configuración regional de cualquier script PHP no es la misma que la del sistema, puede que tenga que especificar la configuración regional en los scripts de PHP mediante una llamada a la función integrada [setlocale](https://www.php.net/manual/en/function.setlocale.php) de PHP. 

Por ejemplo, si el valor predeterminado del sistema es `en_US.UTF-8`, pero el script PHP usa `de_DE.UTF-8`, llame a la función `setlocale()` de PHP como corresponde.

Para la opción 2, indique la configuración regional deseada en los scripts PHP solo si es diferente de la variable `LC_ALL`.

> [!NOTE]
> Si no se define nada en php.ini, el valor predeterminado actual es invalidar todos los demás valores de configuración regional basados en `LC_ALL`, que quedará **en desuso**. En un futuro próximo, el valor predeterminado será omitir la configuración regional del sistema. Por lo tanto, los usuarios tendrán que modificar el archivo php.ini en consecuencia si quieren mantener el comportamiento actual.

Si los controladores sqlsrv y pdo_sqlsrv están habilitados, no se recomienda establecer diferentes opciones para los dos controladores.
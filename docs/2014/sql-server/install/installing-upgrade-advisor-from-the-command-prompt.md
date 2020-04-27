---
title: Instalación del Asesor de actualizaciones desde el símbolo del sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- command prompt [Upgrade Advisor]
- Setup [Upgrade Advisor]
- Upgrade Advisor [SQL Server], installing
ms.assetid: a6841cc2-ca13-4b1c-9343-9e4d54312c3a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4b694af5b760ae3c1ead1e4984c35ef61c0fa602
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66094334"
---
# <a name="installing-upgrade-advisor-from-the-command-prompt"></a>Instalar el Asesor de actualizaciones desde el símbolo del sistema
  Puede instalar el Asesor de actualizaciones mediante el Asistente para instalación o desde el símbolo del sistema. Mediante el símbolo del sistema, podrá realizar instalaciones desatendidas y automatizadas.  
  
## <a name="installation-syntax"></a>Sintaxis de la instalación  
 La sintaxis básica para instalar el Asesor de actualizaciones desde el símbolo del sistema es como sigue:  
  
 `SQLUA.msi [options]`  
  
 En la tabla siguiente se muestran las opciones más comunes.  
  
|Argumento|Descripción|  
|--------------|-----------------|  
|/q [n&#124;b&#124;r&#124;f]|Establece el nivel de la interfaz de usuario (UI):<br /><br /> n = sin interfaz de usuario<br /><br /> b = interfaz de usuario básica (solo progresos, sin interacción)<br /><br /> r = interfaz de usuario reducida (cuadro de diálogo al final de la instalación)<br /><br /> f = interfaz de usuario completa|  
|/L|Especifica las opciones del archivo de registro. Para registrar todos los mensajes en *log_file_name*, use **-\*L v**_log_file_name_. Para registrar solo los mensajes de error `-Le`, use *log_file_name*.|  
|ADDLOCAL = ALL&#124; REMOVE = ALL&#124;REINSTALL = ALL|Se usa para instalar (ADDLOCAL), quitar (REMOVE) o reinstalar (REINSTALL) el Asesor de actualizaciones.|  
|UAINSTALLDIR=ruta|Instala el Asesor de actualizaciones en la ubicación especificada por la ruta.|  
  
## <a name="installation-examples"></a>Ejemplos de instalación  
 El ejemplo siguiente muestra cómo instalar el Asesor de actualizaciones utilizando el símbolo del sistema:  
  
```  
SQLUA.msi /qn ADDLOCAL=ALL UAINSTALLDIR="C:\Upgrade Advisor"  
```  
  
 También puede utilizar el programa Msiexec para ejecutar este comando:  
  
```  
Msiexec.exe /i C:\Downloads\SQLUA.msi /qn ADDLOCAL=ALL UAINSTALLDIR="C:\Upgrade Advisor"  
```  
  
 Esto puede resultar útil si tiene que utilizar opciones de instalación adicionales.  
  
## <a name="removal-examples"></a>Ejemplos de eliminación  
 El ejemplo siguiente muestra cómo eliminar el Asesor de actualizaciones utilizando el símbolo del sistema:  
  
```  
SQLUA.msi /qn REMOVE=ALL  
```  
  
 También puede utilizar el programa Msiexec para ejecutar este comando:  
  
```  
Msiexec.exe /i C:\Downloads\SQLUA.msi /qn REMOVE=ALL  
```  
  
## <a name="see-also"></a>Consulte también  
 [Instalando el asesor de actualizaciones](../../../2014/sql-server/install/installing-upgrade-advisor.md)   
 [Requisitos previos del Asesor de actualizaciones](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md)  
  
  

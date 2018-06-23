---
title: Instalar el Asesor de actualizaciones desde el símbolo del sistema | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- installing Upgrade Advisor
- command prompt [Upgrade Advisor]
- Setup [Upgrade Advisor]
- Upgrade Advisor [SQL Server], installing
ms.assetid: a6841cc2-ca13-4b1c-9343-9e4d54312c3a
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8433aa58002095568a79013ec398f96f87abd22b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198345"
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
|/L|Especifica las opciones del archivo de registro. Para registrar todos los mensajes en *log_file_name*, utilice **-L\*v *** nombre_archivo_registro*. Para registrar solo mensajes de error, use `-Le` *log_file_name*.|  
|ADDLOCAL = ALL&AMP;#124; QUITAR = ALL&AMP;#124;REINSTALL = ALL|Se usa para instalar (ADDLOCAL), quitar (REMOVE) o reinstalar (REINSTALL) el Asesor de actualizaciones.|  
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
  
## <a name="see-also"></a>Vea también  
 [Instalar el Asesor de actualizaciones](../../../2014/sql-server/install/installing-upgrade-advisor.md)   
 [Requisitos previos del Asesor de actualizaciones](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md)  
  
  
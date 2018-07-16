---
title: Rol de instalación | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c7e9db15-89f2-4d4d-8860-1e64c5821c4d
caps.latest.revision: 14
author: heidisteen
ms.author: heidist
manager: craigg
ms.openlocfilehash: 6b37c8749ee82894ee7c28acf6b0fa94bf4ee58f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37330985"
---
# <a name="setup-role"></a>Rol de instalación
  Utilice esta página para especificar si utilizar la página Selección de características para seleccionar características individuales o para instalar utilizando un rol de instalación.  
  
 Un `setup role` es una selección fija de todas las características y componentes compartidos que se necesitan para implementar una configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] predefinida.  
  
## <a name="options"></a>Opciones  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instalación de características**  
 Elija esta opción para seleccionar características individuales y componentes compartidos. Entre las características de instancia se incluyen Servicios de Motor de base de datos, Analysis Services (modo nativo) y Reporting Services.  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Modelo de objetos de informe utilizado por las extensiones de representación.**  
 Elija esta opción para instalar los componentes de servidor de Analysis Services en una granja de SharePoint 2010. Esta opción implementa el servicio de Sistema de PowerPivot y el servidor de Analysis Services en una granja de servidores, lo que habilita el procesamiento de datos y consultas a gran escala para los libros de Excel publicados que contienen datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] incrustados.  
  
 De manera opcional, puede agregar una instancia de motor de base de datos relacional a la instalación en caso que sea necesario hospedar bases de datos en una granja de servidores SharePoint. Si la granja de servidores ya está configurada, puede omitir esta opción.  
  
 Una vez finalizada la instalación, deberá configurar el software mediante uno de los métodos siguientes: herramienta de configuración de PowerPivot, cmdlets de PowerShell o SharePoint 2010 Central Administration. A diferencia de las versiones anteriores, la instalación ya no realiza ninguna tarea de configuración para una instalación de PowerPivot.  
  
 Una instalación basada en roles no incluye la aplicación cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerPivot para Excel. La aplicación cliente se instala por separado.  
  
 **Todas las funciones con valores predeterminados**  
 Elija este rol de instalación para instalar todas las características que están disponibles para esta versión. Observe que PowerPivot para SharePoint se excluye de este rol. Debe utilizar el rol de instalación de PowerPivot para SharePoint para instalar esa característica.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] está configurado para empezar a usar la cuenta **NT AUTHORITY\NETWORK SERVICE**. El usuario actual se aprovisionará como un miembro del rol [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**de** . Los valores establecidos por esta opción se pueden invalidar especificando otros parámetros de línea de comandos.  
  
 Cuando el sistema operativo no sea un controlador de dominio, de forma predeterminada, Reporting Services y el Motor de base de datos utilizarán la cuenta NTAUTHORITY\NETWORK SERVICE, Integration Services utilizará la cuenta NTAUTHORITY\NETWORK SERVICE y el selector de demonio de filtro de texto completo de SQL utilizará la cuenta NTAUTHORITY\LOCAL SERVICE.  
  
## <a name="see-also"></a>Vea también  
 [Instalar PowerPivot para SharePoint](http://go.microsoft.com/fwlink/?LinkId=206906)   
 [Requisitos de hardware y Software (PowerPivot para SharePoint](http://go.microsoft.com/fwlink/?LinkId=216823)   
 [Selección de características](../../../2014/sql-server/install/feature-selection.md)  
  
  

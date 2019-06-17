---
title: Rol de instalación | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: c7e9db15-89f2-4d4d-8860-1e64c5821c4d
author: heidisteen
ms.author: heidist
manager: craigg
ms.openlocfilehash: b1cf8c6f8442fc69669c10106f671040733e48ef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092232"
---
# <a name="setup-role"></a>Rol de instalación
  Utilice esta página para especificar si utilizar la página Selección de características para seleccionar características individuales o para instalar utilizando un rol de instalación.  
  
 Un `setup role` es una selección fija de todas las características y componentes compartidos que se necesitan para implementar una configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] predefinida.  
  
## <a name="options"></a>Opciones  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instalación de características**  
 Elija esta opción para seleccionar características individuales y componentes compartidos. Entre las características de instancia se incluyen Servicios de Motor de base de datos, Analysis Services (modo nativo) y Reporting Services.  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerPivot para SharePoint**  
 Elija esta opción para instalar los componentes de servidor de Analysis Services en una granja de SharePoint 2010. Esta opción implementa el servicio de Sistema de PowerPivot y el servidor de Analysis Services en una granja de servidores, lo que habilita el procesamiento de datos y consultas a gran escala para los libros de Excel publicados que contienen datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] incrustados.  
  
 De manera opcional, puede agregar una instancia de motor de base de datos relacional a la instalación en caso que sea necesario hospedar bases de datos en una granja de servidores SharePoint. Si la granja de servidores ya está configurada, puede omitir esta opción.  
  
 Una vez finalizada la instalación, debe configurar el software mediante uno de los métodos siguientes: Herramienta de configuración de PowerPivot, cmdlets de PowerShell o Administración Central de SharePoint 2010. A diferencia de las versiones anteriores, la instalación ya no realiza ninguna tarea de configuración para una instalación de PowerPivot.  
  
 Una instalación basada en roles no incluye la aplicación cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerPivot para Excel. La aplicación cliente se instala por separado.  
  
 **Todas las funciones con valores predeterminados**  
 Elija este rol de instalación para instalar todas las características que están disponibles para esta versión. Observe que PowerPivot para SharePoint se excluye de este rol. Debe utilizar el rol de instalación de PowerPivot para SharePoint para instalar esa característica.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] está configurado para empezar a usar la cuenta **NT AUTHORITY\NETWORK SERVICE**. El usuario actual se aprovisionará como un miembro del rol [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**de** . Los valores establecidos por esta opción se pueden invalidar especificando otros parámetros de línea de comandos.  
  
 Cuando el sistema operativo no sea un controlador de dominio, de forma predeterminada, Reporting Services y el Motor de base de datos utilizarán la cuenta NTAUTHORITY\NETWORK SERVICE, Integration Services utilizará la cuenta NTAUTHORITY\NETWORK SERVICE y el selector de demonio de filtro de texto completo de SQL utilizará la cuenta NTAUTHORITY\LOCAL SERVICE.  
  
## <a name="see-also"></a>Vea también  
 [Instalar PowerPivot para SharePoint](https://go.microsoft.com/fwlink/?LinkId=206906)   
 [Requisitos de hardware y Software (PowerPivot para SharePoint](https://go.microsoft.com/fwlink/?LinkId=216823)   
 [Selección de características](../../../2014/sql-server/install/feature-selection.md)  
  
  

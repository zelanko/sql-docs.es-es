---
title: Opciones (resultados de la consulta y página de servicios de dependencia) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryResults.DependencyServicesGeneral
ms.assetid: dd7f6c31-7d7f-4972-854a-1419a2826dca
caps.latest.revision: 6
author: mashamsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ecc1b6d238189ca0b9c33dd97d136d3283f1ae6b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37192105"
---
# <a name="options-query-results-and-dependency-services-page"></a>Opciones (resultados de la consulta y página de servicios de dependencia)
  Utilice esta página para especificar el servidor al que desea conectarse para Servicios de dependencia. Servicios de dependencia le permite extraer información sobre las dependencias existentes entre los objetos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] y los de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] almacenados en servidores diferentes. Ver las dependencias del objeto mediante el **dependencias del objeto** cuadro de diálogo de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
  
 **¿Qué desea hacer?**  
  
1.  [Abra el cuadro de diálogo Opciones (página de servicios de dependencia/resultados de consulta)](#open_dialog)  
  
2.  [Configurar las opciones](#options)  
  
##  <a name="open_dialog"></a> Abra el cuadro de diálogo Opciones (página de servicios de dependencia/resultados de consulta)  
  
1.  En [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], haga clic en **opciones** en el **herramientas** menú.  
  
2.  Expanda **Resultados de la consulta** y, después, haga clic en **Servicios de dependencia**.  
  
##  <a name="options"></a> Configurar las opciones  
  
### <a name="options"></a>Opciones  
 **Servidor de servicios de dependencia**  
 Especifique el servidor en el que está instalado Servicios de dependencia.  
  
 **Autenticación**  
 Seleccione Autenticación de Windows para iniciar sesión con una cuenta de usuario de Microsoft Windows o seleccione Autenticación de SQL Server.  
  
 Cuando un usuario se conecta con un nombre y una contraseña de inicio de sesión determinados desde una conexión que no es de confianza, SQL Server realiza la autenticación y comprueba si se ha configurado una cuenta de inicio de sesión de SQL Server y si la contraseña especificada coincide con la almacenada anteriormente. Si SQL Server no encuentra la cuenta de inicio de sesión, la autenticación no se realizará correctamente y el usuario recibirá un mensaje de error.  
  
 **Nombre de usuario.**  
 Si utiliza Autenticación de SQL Server, proporcione un nombre de usuario.  
  
 **Contraseña**  
 Si está utilizando Autenticación de SQL Server, proporcione una contraseña.  
  
 **Prueba**  
 Haga clic en esta opción para comprobar la conexión.  
  
  

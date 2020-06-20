---
title: Opciones (página resultados de la consulta y servicios de dependencia) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryResults.DependencyServicesGeneral
ms.assetid: dd7f6c31-7d7f-4972-854a-1419a2826dca
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d19228fdf17788e9118367a6f0f0eb3be90cb72a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84930137"
---
# <a name="options-query-results-and-dependency-services-page"></a>Opciones (Resultados de la consulta/página Servicios de dependencia)
  Utilice esta página para especificar el servidor al que desea conectarse para Servicios de dependencia. Servicios de dependencia le permite extraer información sobre las dependencias existentes entre los objetos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] y los de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] almacenados en servidores diferentes. Puede ver las dependencias de los objetos mediante el cuadro de diálogo **dependencias del objeto** de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] .  
  
 **¿Qué desea hacer?**  
  
1.  [Abrir el cuadro de diálogo Opciones (página Resultados de la consulta/Servicios de dependencia)](#open_dialog)  
  
2.  [Configurar las opciones](#options)  
  
##  <a name="open-the-options-query-resultsdependency-services-page-dialog-box"></a><a name="open_dialog"></a>Abrir el cuadro de diálogo Opciones (página resultados de la consulta/servicios de dependencia)  
  
1.  En [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] , haga clic en **Opciones** en el menú **herramientas** .  
  
2.  Expanda **Resultados de la consulta** y, después, haga clic en **Servicios de dependencia**.  
  
##  <a name="configure-the-options"></a><a name="options"></a>Configurar las opciones  
  
### <a name="options"></a>Opciones  
 **Servidor de los servicios de dependencia.**  
 Especifique el servidor en el que está instalado Servicios de dependencia.  
  
 **Autenticación**  
 Seleccione Autenticación de Windows para iniciar sesión con una cuenta de usuario de Microsoft Windows o seleccione Autenticación de SQL Server.  
  
 Cuando un usuario se conecta con un nombre y una contraseña de inicio de sesión determinados desde una conexión que no es de confianza, SQL Server realiza la autenticación y comprueba si se ha configurado una cuenta de inicio de sesión de SQL Server y si la contraseña especificada coincide con la almacenada anteriormente. Si SQL Server no encuentra la cuenta de inicio de sesión, la autenticación no se realizará correctamente y el usuario recibirá un mensaje de error.  
  
 **Nombre de usuario**  
 Si utiliza Autenticación de SQL Server, proporcione un nombre de usuario.  
  
 **Contraseña**  
 Si está utilizando Autenticación de SQL Server, proporcione una contraseña.  
  
 **Prueba**  
 Haga clic en esta opción para comprobar la conexión.
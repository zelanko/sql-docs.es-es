---
title: Crear un modelo mediante Administrador de informes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report models [Reporting Services], creating
- Report Manager [Reporting Services], model creation
ms.assetid: 8e5d2bd3-48ec-45f3-afee-6d86797c8f28
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7b67e2a7048520d8a411789e501dbbe545d3cc02
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109672"
---
# <a name="create-a-model-using-report-manager"></a>Crear un modelo con el Administrador de informes
  Puede generar modelos a partir de un cubo de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , una base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o una base de datos de Oracle mediante el Administrador de informes. Los modelos de informe se generan a partir de orígenes de datos compartidos que se han publicado en el servidor de informes. Si no tiene un origen de datos compartido, deberá crearlo.  
  
 El modelo de informe que se genera se basa completamente en el esquema del origen de datos compartido. No puede elegir qué partes del origen de datos se incluyen en el modelo, ni puede editar las reglas o metadatos de un modelo generado. Sin embargo, puede establecer las propiedades del modelo después de que se haya generado y definir las asignaciones de roles que restrinjan el acceso a todo el modelo o parte de él.  
  
> [!NOTE]  
>  Un modelo basado en Oracle generado mediante administrador de informes o [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[offSPServ](../includes/offspserv-md.md)] 2007 [!INCLUDE[SPS2010](../includes/sps2010-md.md)] incluirá objetos de base de datos que forman parte del esquema de la cuenta de usuario utilizada para conectarse al origen de datos de Oracle. El nombre de la cuenta de usuario está especificado en las credenciales de propiedades del origen de datos.  
  
### <a name="to-create-a-new-data-source-for-a-report-model-using-report-manager"></a>Para crear un nuevo origen de datos para un modelo de informe con el Administrador de informes  
  
1.  En el explorador web, escriba la dirección URL del servidor de informes en la barra de direcciones.  
  
2.  Haga clic en **Nuevo origen de datos**.  
  
3.  En el cuadro **Nombre** , escriba un nombre para el origen de datos.  
  
4.  Opcionalmente, escriba una breve descripción del modo en el cuadro de texto **Descripción** .  
  
5.  Compruebe que la casilla **Habilitar este origen de datos** está activada.  
  
6.  En la lista **Tipo de conexión** , seleccione el tipo de origen de datos al que desea conectarse. El tipo de conexión debe ser uno de los siguientes: **Oracle**, **Microsoft SQL Server** o **Microsoft SQL Server Analysis Services**.  
  
7.  En el cuadro **Cadena de conexión** , escriba la cadena de conexión que apunta a la base de datos.  
  
8.  Seleccione el método de conexión que utilizarán los usuarios del Generador de informes para conectarse a la base de datos.  
  
    -   Autenticación de Windows: seleccione esta opción cuando desee que el sistema operativo autentique a los usuarios de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Esta opción permite que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utilice las características de seguridad de Windows, como el cifrado de contraseñas, para autenticar a los usuarios. Se recomienda encarecidamente seleccionar esta opción.  
  
    -   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Autenticación: Seleccione esta opción si desea que los usuarios utilicen una [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cuenta de inicio de sesión que haya creado. Los usuarios deben proporcionar un nombre y una contraseña de inicio de sesión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] válidos.  
  
        > [!CAUTION]  
        >  Siempre que sea posible, utilice la autenticación de Windows.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-create-a-report-model-using-report-manager"></a>Para crear un modelo de informe mediante el Administrador de informes  
  
1.  En el Administrador de informes, seleccione el origen de datos que desee usar para el modelo.  
  
     Se muestra la página Propiedades.  
  
2.  Compruebe que desea utilizar las opciones especificadas para el origen de datos.  
  
3.  Haga clic en **Generar modelo**.  
  
     Se muestra la página General para el origen de datos.  
  
4.  En el cuadro **Nombre** , escriba un nombre para el modelo de informe.  
  
5.  En el cuadro **Descripción** , escriba una breve descripción para el modelo.  
  
6.  Para especificar una nueva ubicación en la que guardar el modelo de informe, haga clic en **Cambiar ubicación**.  
  
     De manera predeterminada, el modelo de informe se guarda en la página Inicio del Administrador de informes.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     El modelo de informe se crea y guarda en la ubicación que especificó. Puede asignar los permisos a este modelo con el Administrador de informes.  
  
## <a name="see-also"></a>Consulte también  
 [Conceder permisos en un servidor de informes en modo nativo](security/granting-permissions-on-a-native-mode-report-server.md)   
 [Conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Nuevo origen de datos &#40;página del Administrador de informes&#41;](../../2014/reporting-services/new-data-source-page-report-manager.md)  
  
  

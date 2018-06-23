---
title: Crear, eliminar o modificar un origen de datos compartido (Administrador de informes) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- shared data sources [Reporting Services]
- removing shared data sources
- data sources [Reporting Services], shared
- deleting shared data sources
- modifying shared data sources
ms.assetid: cd7bace3-f8ec-4ee3-8a9f-2f217cdca9f2
caps.latest.revision: 47
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 0f5f9b5397d1f50e460f4f8f483daa7a9b3ef23f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108041"
---
# <a name="create-delete-or-modify-a-shared-data-source-report-manager"></a>Crear, eliminar o modificar un origen de datos compartido (Administrador de informes)
  Un origen de datos compartido especifica las propiedades de conexión para un origen de datos. Si tiene un origen de datos usado por un gran número de informes, modelos o suscripciones controladas por datos, piense en crear un origen de datos compartido para eliminar la sobrecarga de tener que mantener la misma información de conexión en varios lugares.  
  
 El siguiente icono indica que existe un origen de datos compartido en la jerarquía de carpetas del Administrador de informes:  
  
 ![Icono de origen de datos compartido](media/hlp-16datasource.png "Icono de origen de datos compartido")  
Icono de origen de datos compartido  
  
### <a name="to-create-a-shared-data-source"></a>Para crear un origen de datos compartido  
  
1.  Inicie el [Administrador de informes &#40;Modo nativo de SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md).  
  
2.  En el Administrador de informes, navegue hasta la página **Contenido** .  
  
3.  Haga clic en **Nuevo origen de datos**. Se abre la página **Nuevo origen de datos** .  
  
4.  Escriba el nombre del elemento. El nombre debe incluir al menos un carácter y debe empezar con una letra. También puede incluir determinados símbolos, pero no espacios en blanco o los caracteres ; ? : @ & = +, $ / * \< > | " /.  
  
5.  Si lo desea, escriba una descripción que ofrezca a los usuarios información sobre la conexión. Esta descripción aparecerá en la página **Contenido** del Administrador de informes.  
  
6.  En la lista **Tipo de origen de datos** , especifique la extensión de procesamiento de datos que se utiliza para procesar datos desde el origen de datos.  
  
7.  En **Cadena de conexión**, especifique la cadena de conexión que utiliza el servidor de informes para conectarse al origen de datos. Se recomienda que no especifique credenciales en la cadena de conexión.  
  
     En el ejemplo siguiente se muestra una cadena de conexión para conectarse a la variable local [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] base de datos:  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
8.  En **Conectar utilizando**, especifique cómo se obtienen las credenciales cuando se ejecuta el informe:  
  
    -   Si desea solicitar al usuario un nombre de inicio de sesión y una contraseña, haga clic en **Credenciales suministradas por el usuario que ejecuta el informe**. Para utilizar las credenciales que el usuario especifica como credenciales de Windows, active la casilla **Utilizar como credenciales de Windows para la conexión al origen de datos**. Si el nombre de usuario y la contraseña son las credenciales de la base de datos, no active esta opción.  
  
    -   Si va a usar el origen de datos para que se comparta con credenciales guardadas administradas por el propietario del origen de datos, o con informes que admitan suscripciones u otras operaciones programadas (por ejemplo, la generación automatizada de historiales de informes), haga clic en **Credenciales almacenadas de forma segura en el servidor de informes**. Si el servidor de bases de datos admite la suplantación o la delegación, puede seleccionar **Suplantar al usuario autenticado después de realizar una conexión al origen de datos**.  
  
    -   Si desea que el servidor de informes envíe las credenciales del usuario que tiene acceso al informe al servidor que hospeda el origen de datos externo, haga clic en **Seguridad integrada de Windows NT**. En este caso, no se solicita al usuario que escriba un nombre de usuario ni una contraseña.  
  
    -   Si el origen de datos no usa credenciales (por ejemplo, si el origen de datos es un archivo XML al que se tiene acceso desde el sistema de archivos), haga clic en **No se necesitan credenciales**. Solo debería especificar este tipo de credencial si es válido para el origen de datos. Si selecciona esta opción para un origen de datos que requiere autenticación, se producirá un error en la conexión. Si selecciona esta opción, asegúrese de que configura la cuenta de ejecución desatendida que permite al servidor de informes conectar a otros equipos para recuperar datos o archivos cuando las credenciales del usuario no están disponibles.  
  
     Para obtener más información acerca de cómo configurar las credenciales, vea [especificar credenciales y la información de conexión para orígenes de datos de informe](report-data/specify-credential-and-connection-information-for-report-data-sources.md). Para más información sobre la cuenta de ejecución desatendida, vea [Configurar la cuenta de ejecución desatendida &#40;Administrador de configuración de SSRS&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
9. Haga clic en el botón **Probar conexión** para validar la configuración del origen de datos.  
  
    > [!NOTE]  
    >  El botón Probar conexión no se admite para el tipo de origen de datos XML.  
  
10. Haga clic en **Aceptar**.  
  
### <a name="to-modify-a-shared-data-source"></a>Para modificar un origen de datos compartido  
  
1.  En el Administrador de informes, navegue a la página Contenido.  
  
2.  Navegue al elemento de orígenes de datos compartidos, mantenga el mouse sobre el elemento, haga clic en la lista desplegable y seleccione **Administrar**en el menú contextual. Se abre la página **Propiedades** .  
  
3.  Modifique el origen de datos y, a continuación, haga clic en **Aplicar**.  
  
### <a name="to-delete-a-shared-data-source"></a>Para eliminar un origen de datos compartido  
  
-   En el Administrador de informes, navegue a la página **Contenido** y realice una de las siguientes acciones:  
  
    -   Navegue al elemento de origen de datos compartido.  
  
         Haga clic en el elemento para abrirlo. Se abre la página de propiedades General.  
  
         Haga clic en **Eliminar**y, después, en **Aceptar**.  
  
    -   En la página **Contenido** , navegue a la carpeta que contiene el origen de datos que desea eliminar.  
  
         Mantenga el mouse sobre el elemento, haga clic en la lista desplegable y seleccione **Eliminar** en el menú contextual.  
  
         [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Las conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [El contenido de página &#40;el Administrador de informes&#41;](../../2014/reporting-services/contents-page-report-manager.md)   
 [Crear, modificar y eliminar orígenes de datos compartidos &#40;SSRS&#41;](report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
 [Administrar los orígenes de datos de informe](report-data/manage-report-data-sources.md)   
 [Configurar las propiedades del origen de datos para un informe &#40;el Administrador de informes&#41;](report-data/configure-data-source-properties-for-a-report-report-manager.md)  
  
  
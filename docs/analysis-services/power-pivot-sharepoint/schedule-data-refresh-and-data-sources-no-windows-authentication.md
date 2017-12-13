---
title: "Programación de actualización de datos y orígenes de datos, sin autenticación de Windows | Documentos de Microsoft"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d8d875bc-7823-46b7-a939-867cefd4de12
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c165409874271ef7ab60428976f74212a3b3f431
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="schedule-data-refresh-and-data-sources---no-windows-authentication"></a>Programación de actualización de datos y orígenes de datos, sin autenticación de Windows
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Este tema describe un flujo de trabajo de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint nuevos datos de programación que pueden usar datos de orígenes que **no** compatible con la autenticación de Windows. Por ejemplo, orígenes de datos Oracle o IBM DB2. Las ilustraciones y los pasos de este tema hacen referencia a orígenes de datos Oracle, pero se aplica el mismo flujo de trabajo a otros orígenes de datos.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010 &#124; SharePoint 2013.|  
  
 **Información general:** Cree dos aplicaciones de destino de almacenamiento seguro Configure la primera aplicación de destino (PowerPivotDataRefresh) para usar las credenciales de Windows. Configure la segunda aplicación de destino con las credenciales para un origen de datos que no admita la autenticación de Windows, por ejemplo, una base de datos Oracle. La segunda aplicación de destino también usa la primera aplicación de destino para la cuenta de actualización de datos desatendida.  
  
 ![as_powerpivot_refresh_no_windows_auth](../../analysis-services/power-pivot-sharepoint/media/as-powerpivot-refresh-no-windows-auth.gif "as_powerpivot_refresh_no_windows_auth")  
  
-   **(1) PowerPivotDatarefresh:** Un identificador de aplicación de destino de almacén seguro que se establece con la autenticación de Windows.  
  
-   **(2) OracleAuthentication:** Un identificador de aplicación de destino de almacén seguro que se establece con las credenciales de Oracle.  
  
-   **(3)** La aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] está configurada para usar la aplicación de destino "PowerPivotDataRefresh" para la **cuenta de actualización de datos desatendida**.  
  
-   **(4)** El libro de PowerPivot usa datos de Oracle. Los valores de actualización del libro especifican la conexión de origen de datos que usa la aplicación de destino **(2)** para las credenciales.  
  
## <a name="prerequisites"></a>Requisitos previos  
  
-   Existe una aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
-   Existe una aplicación de servicio de almacenamiento seguro.  
  
-   Existe un libro de Excel con un modelo de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
## <a name="to-create-a-target-application-id-that-uses-windows-authentication"></a>Para crear un identificador de aplicación de destino que use la autenticación de Windows  
  
1.  En Administración central de SharePoint, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Haga clic en el nombre de la aplicación de servicio de almacenamiento seguro.  
  
3.  En la página **Administrar** , haga clic en **Nuevo**. ![as_powerpivot_refresh_sss_new_target_application](../../analysis-services/power-pivot-sharepoint/media/as-powerpivot-refresh-sss-new-target-application.gif "as_powerpivot_refresh_sss_new_target_application")  
  
4.  En la página **Crear nueva aplicación de destino de almacenamiento seguro** , configure los valores siguientes:  
  
    -   **Identificador de la aplicación de destino:** PowerPivotDataRefresh.  
  
    -   **Nombre para mostrar:** PowerPivotDataRefresh.  
  
    -   **Correo electrónico de contacto:** ?  
  
    -   **Tipo de aplicación de destino:** Grupo.  
  
    -   **Dirección URL de la página de la aplicación de destino:** Ninguna.  
  
5.  Haga clic en **Siguiente**.  
  
6.  En la página Credenciales, deje los dos valores predeterminados de nombre de campo y tipos de campo para **Nombre de usuario Windows** y **Contraseña de Windows**.  
  
7.  Haga clic en **Siguiente**.  
  
8.  En la página **Configuración de pertenencia** , agregue al menos un **Administrador de aplicación de destino** y, a continuación, agregue los miembros que necesiten acceso a la aplicación de destino.  
  
9. Haga clic en **Aceptar**.  
  
10. El nuevo identificador de aplicación de destino se agrega a la lista. Seleccione el identificador de aplicación de destino y haga clic en **establecer credenciales**![as_powerpivot_refresh_sss_set_key](../../analysis-services/power-pivot-sharepoint/media/as-powerpivot-refresh-sss-set-key.gif "as_powerpivot_refresh_sss_set_key").  
  
11. Escriba el nombre de usuario Windows y la contraseña de Windows y, a continuación, haga clic en **Aceptar**.  
  
## <a name="to-create-a-target-application-id-that-uses-oracle-credentials"></a>Para crear un identificador de aplicación de destino que use las credenciales de Oracle  
  
1.  En Administración central de SharePoint, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Haga clic en el nombre de la aplicación de servicio de almacenamiento seguro.  
  
3.  En el **administrar** página, haga clic en **New**![as_powerpivot_refresh_sss_new_target_application](../../analysis-services/power-pivot-sharepoint/media/as-powerpivot-refresh-sss-new-target-application.gif "as_powerpivot_refresh_sss_new_target_application ").  
  
4.  En la página **Crear nueva aplicación de destino de almacenamiento seguro** , configure los valores siguientes:  
  
    -   **Identificador de aplicación de destino:** OracleAuthentication.  
  
    -   **Nombre para mostrar:** OracleAuthentication.  
  
    -   **Correo electrónico de contacto:** ?  
  
    -   **Tipo de aplicación de destino:** Grupo.  
  
    -   **Dirección URL de la página de la aplicación de destino:** Ninguna.  
  
5.  Haga clic en **Siguiente**.  
  
6.  En la página **Credenciales** , cambie el primer nombre de campo a **Oracle User ID** y cambie el **Tipo de campo** a **User Name**.  
  
     Cambie el segundo nombre de campo a **Oracle Password** y el **Tipo de campo** a **Password**.  
  
7.  Haga clic en **Siguiente**.  
  
8.  En la página **Configuración de pertenencia** , agregue al menos un **Administrador de aplicación de destino** y, a continuación, agregue los miembros que necesiten acceso a la aplicación de destino.  
  
9. Haga clic en **Aceptar**.  
  
10. El nuevo identificador de aplicación de destino se agrega a la lista. Seleccione el identificador de aplicación de destino y haga clic en **establecer credenciales**![as_powerpivot_refresh_sss_set_key](../../analysis-services/power-pivot-sharepoint/media/as-powerpivot-refresh-sss-set-key.gif "as_powerpivot_refresh_sss_set_key").  
  
11. Escriba el identificador de usuario Oracle y la contraseña de Oracle y, a continuación, haga clic en **Aceptar**.  
  
 Para más información, vea la sección sobre cómo crear una aplicación de destino para la autenticación de SQL Server en [Usar almacenamiento seguro con la autenticación de SQL Server (SharePoint Server 2013)](http://technet.microsoft.com/library/gg298949.aspx) (http://technet.microsoft.com/library/gg298949.aspx).  
  
## <a name="to-configure-the-power-pivot-service-application"></a>Para configurar la aplicación de servicio Power Pivot  
  
1.  En Administración central de SharePoint, haga clic en Administrar aplicaciones de servicio.  
  
2.  Haga clic en el nombre de la aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , por ejemplo "Aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] predeterminada".  
  
3.  Haga clic en **Configurar las opciones de aplicación de servicio** en la sección Acciones.  
  
4.  En la sección **Actualización de datos**, establezca la **Cuenta de actualización de datos desatendida de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]** en **PowerPivotDataRefresh** y haga clic en **Aceptar**.  
  
     ![as_powerpivot_refresh_new_refresh_acount](../../analysis-services/power-pivot-sharepoint/media/as-powerpivot-refresh-new-refresh-acount.gif "as_powerpivot_refresh_new_refresh_acount")  
  
## <a name="to-configure-the-workbook"></a>Para configurar el libro  
  
1.  Busque el libro en el [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] galería y haga clic en **administrar actualización de datos**![as_powerpivot_refresh_manage_reresh](../../analysis-services/power-pivot-sharepoint/media/as-powerpivot-refresh-manage-reresh.gif "as_powerpivot_refresh_manage_reresh").  
  
2.  Si aparece la página **Historial de actualización de datos** , haga clic en **Configurar programación**.  
  
3.  Haga clic en **Habilitar**.  
  
4.  Haga clic en **También actualizar lo más rápido posible**.  
  
5.  En la sección **Credenciales** , haga clic en **Usar la cuenta de actualización de datos configurada por el administrador**.  
  
6.  Desactive **Todos los orígenes de datos**.  
  
7.  Seleccione **Actualizar** para el origen de datos que usa los datos Oracle. El nombre del origen de datos puede cambiarse en Microsoft Excel en el menú **Datos**, **Conexiones**, **Propiedades** .  
  
8.  En el origen de datos, seleccione **Usar programación predeterminada**.  
  
9. Seleccione **Conectar con las credenciales guardadas en el servicio de almacenamiento seguro (SSS) para iniciar sesión en el origen de datos. Especifique el identificador usado para buscar las credenciales en el cuadro de identificador de SSS**.  
  
10. En el cuadro **Id.:** , escriba **OracleAuthentication**.  
  
11. Haga clic en **Aceptar**.  
  
     Si se muestra un mensaje de error similar al siguiente: `The provided Secure Store target application is either incorrectly configured or does not exist`.  
  
     Las dos soluciones comunes son:  
  
    -   Compruebe que el identificador de la aplicación de destino es correcto.  
  
    -   Compruebe que ha establecido las credenciales para la aplicación de destino.  
  
## <a name="to-verify-data-refresh-with-the-new-authentication"></a>Para comprobar la actualización de datos con la nueva autenticación  
 Cuando haga clic en **Aceptar**, se mostrará la página **Historial de actualización** . En unos pocos minutos, debe aparecer un nuevo elemento en el historial de actualización porque en los pasos anteriores seleccionó **También actualizar lo más rápido posible**. El valor predeterminado para el trabajo del temporizador **Trabajo de temporizador de actualización de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]** es 1 minuto. Si no aparece un nuevo elemento en el historial de actualización, espere unos minutos y actualice el explorador. Si todavía no aparece el nuevo elemento, compruebe el valor actual de trabajo del temporizador.  
  
## <a name="more-information"></a>Más información  
  
-   [Configurar el Servicio de almacenamiento seguro de SharePoint 2013](http://technet.microsoft.com/library/ee806866.aspx).  
  
-   Vea la sección "Actualización de datos programada" de [Actualización de datos de Power Pivot con SharePoint 2013 y SQL Server 2012 SP1 (Analysis Services)](http://msdn.microsoft.com/library/jj879294.aspx#bkmk_windows_auth_interactive_data_refresh).  
  
  

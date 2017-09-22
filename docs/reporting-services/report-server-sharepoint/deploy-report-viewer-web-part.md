---
title: Implementar el elemento web Visor de informes en un sitio de SharePoint | Documentos de Microsoft
ms.custom: 
ms.date: 09/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a9397f427cac18d0c8bfc663f6bd477b0440b8a3
ms.openlocfilehash: ed93b0fd5161686becb4cca05c005fd281f2c176
ms.contentlocale: es-es
ms.lasthandoff: 09/15/2017

---

# <a name="deploy-the-report-viewer-web-part-on-a-sharepoint-site"></a>Implementar el elemento web Visor de informes en un sitio de SharePoint

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

El elemento Web de Visor de informes es un elemento Web personalizado que puede usarse para ver informes en SQL Server Reporting Services (modo nativo) dentro de su sitio de SharePoint. Puede usar el elemento Web para ver, navegar, imprimir y exportar informes en un servidor de informes. El elemento Web de Visor de informes está asociado a los archivos de definición (.rdl) de informes que se procesan por un servidor de informes de SQL Server Reporting Services o un servidor de informes de Power BI. Este elemento web Visor de informes de no puede usarse con informes de Power BI hospedados en el servidor de informes de Power BI.

Use las siguientes instrucciones para implementar manualmente el paquete de solución que agregar el elemento web Visor de informes en un entorno de SharePoint Server 2013 o SharePoint Server 2016. Implementación de la solución es un paso necesario para configurar el elemento web.

**El elemento web Visor de informes es un paquete de solución independiente y no está asociado con el modo integrado de SharePoint para SQL Server Reporting Services.**

## <a name="requirements"></a>Requisitos

**Sistemas operativos admitidos:**  
* Windows Server 2008 R2 SP1 y versiones posteriores

**Admite versiones de servidor de SharePoint:**  
* SharePoint Server 2016
* SharePoint Server 2013

**Admite versiones de Reporting Services:**  
* SQL Server 2008 Reporting Services (modo nativo) y versiones posteriores.
* Servidor de informes de Power BI

## <a name="download-the-report-viewer-web-part-solution-package"></a>Descargar el paquete de solución de elementos de web de Visor de informes

El elemento web Visor de informes está disponible en Microsoft Download Center.

[Descargar paquete de solución de elementos de web de Visor de informes](https://www.microsoft.com/en-us/download/details.aspx?id=55949)

## <a name="deploy-the-farm-solution"></a>Implementar la solución de granja de servidores

En esta sección se muestra cómo implementar el paquete de soluciones en la granja de servidores de SharePoint. Esta tarea solo es necesario hacerla una vez.

1. En un servidor de SharePoint, abra un Shell de administración de SharePoint utilizando la **ejecutar como administrador** opción.

2. Ejecutar [Add-SPSolution](https://technet.microsoft.com/library/ff607552(v=office.16).aspx) para agregar la solución de granja de servidores.

    ```
    Add-SPSolution –LiteralPath "{path to file}\ReportViewerWebPart.wsp"
    ```

    El cmdlet devuelve el nombre de la solución, su identificador de solución y Deployed=False. En el paso siguiente, implementará la solución.

3. Ejecute el [Install-SPSolution](https://technet.microsoft.com/library/ff607534(v=office.16).aspx) cmdlet para implementar la solución de granja de servidores.

    **SharePoint 2013**

    ```
    Install-SPSolution –Identity ReportViewerWebPart.wsp -CompatibilityLevel "14,15" -GACDeployment -WebApplication {URL to web application}
    ```

    **SharePoint 2016**

    ```
    Install-SPSolution –Identity ReportViewerWebPart.wsp -GACDeployment -WebApplication {URL to web application}
    ```

## <a name="activate-feature"></a>Activar la característica

1. En el sitio de SharePoint, seleccione la **engranaje** icono en la parte superior izquierda y seleccione **configuración del sitio*.

    ![Configuración del sitio desde el icono de engranaje.](media/sharepoint-site-settings.png)

    De forma predeterminada, se tiene acceso a las aplicaciones web de SharePoint a través del puerto 80. Esto significa que puede acceder a menudo un sitio de SharePoint mediante la especificación de *http://<computer name> * para abrir la colección de sitios raíz.

3. En **administración de colección de sitios**, seleccione **características de colección de sitios**.

4. Desplácese hacia abajo en la página hasta que encuentre el **elemento Web de Visor de informes** característica.

5. Seleccione **Activar**.

    ![Activar la característica de elemento Web de Visor de informes](media/web-part-activiate-feature.png)

6. Repita para colecciones de sitios adicionales abriendo cada sitio y haciendo clic en acciones del sitio.

Si lo desea, también puede usar PowerShell para habilitar esta característica en todos los sitios mediante la [Enable-SPFeature](https://technet.microsoft.com/library/ff607803.aspx) cmdlet.

```
Get-SPWebApplication "<web application url>" | Get-SPSite -Limit ALL | 
        ForEach-Object {
            Write-Host "Enabling feature for $($_.URL)"
            Enable-SPFeature -identity "ReportViewerWebPart" -URL $_.URL -ErrorAction Continue
        }
```

## <a name="remove-the-solution"></a>Quitar la solución

Aunque Administración Central de SharePoint proporciona la retirada de la solución, no necesita retirar el **ReportViewerWebPart.wsp** a menos que esté solucionando problemas de un problema de instalación o una revisión de la implementación de archivos.

1. En Administración Central de SharePoint, en **configuración del sistema**, seleccione **administrar soluciones de granja**.

2. Seleccione **ReportViewerWebPart.wsp**.

3. Seleccione retira solución.

### <a name="remove-the-web-part-from-site-settings"></a>Quite el elemento web de configuración del sitio

Retirar la solución, no se elimina el elemento web Visor de informes en la lista de elementos web dentro de su sitio de SharePoint. Para quitar el elemento web Visor de informes, haga lo siguiente.

1. En el sitio de SharePoint, seleccione la **engranaje** icono en la parte superior izquierda y seleccione **configuración del sitio*.

    ![Configuración del sitio desde el icono de engranaje.](media/sharepoint-site-settings.png)

    De forma predeterminada, se tiene acceso a las aplicaciones web de SharePoint a través del puerto 80. Esto significa que puede acceder a menudo un sitio de SharePoint mediante la especificación de *http://<computer name> * para abrir la colección de sitios raíz.

2. En **galerías del Diseñador Web**, seleccione **elementos Web**.

3. Seleccione el **icono Editar** junto a **ReportViewerNativeMode.dwp**. No puede mostrarse en la primera página de resultados.

4. Seleccione **Eliminar elemento**.

    ![Editar y eliminar el elemento web de modo nativo de Visor de informes](media/report-viewer-native-mode-edit-delete.png)

Eliminación del elemento web puede realizarse mediante el uso de PowerShell, pero no hay un comando directo para él. Para obtener un ejemplo de secuencia de comandos, consulte [cómo eliminar elementos Web de la Galería de elementos Web](https://gallery.technet.microsoft.com/office/How-to-delete-Web-Parts-1132701f).

## <a name="next-steps"></a>Pasos siguientes

Una vez el elemento web se ha implementado el Visor de informes y activa, puede agregar el elemento web a una página de SharePoint. Para obtener más información, consulte [elemento web de agregar el Visor de informes a una página de SharePoint](add-report-viewer-web-part-to-page.md).

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).

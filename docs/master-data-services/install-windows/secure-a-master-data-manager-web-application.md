---
title: Proteger una aplicación web de Master Data Manager | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: e360ba3a-e96b-4f85-b588-ed1f767fa973
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 08e73462f3536f1aff6aecbf44692a7f24f54aa9
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65480172"
---
# <a name="secure-a-master-data-manager-web-application"></a>Proteger una aplicación web Master Data Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Puede proteger la aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] con HTTPS.  
  
> [!NOTE]  
>  La aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] puede usa HTTP o HTTPS, pero no ambos.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar el procedimiento:  
  
-   Debe ser administrador en el servidor web donde está instalado [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .  
  
-   MDS debe estar instalado en el servidor web y debe existir una aplicación web. Para obtener más información, vea [Instalar Master Data Services](../../master-data-services/install-windows/install-master-data-services.md) y [Crear una aplicación web de Master Data Manager &#40;Master Data Services&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md).  
  
### <a name="to-secure-the-master-data-manager-web-application-with-https"></a>Para proteger la aplicación web Administrador de datos maestros con HTTP  
  
1.  Después de confirmar que la aplicación web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] está configurada correctamente con HTTP, cree un certificado en IIS. Para obtener más información, vea [Configurar certificados de servidor en IIS 7](https://technet.microsoft.com/library/cc732230\(WS.10\).aspx).  
  
2.  En el panel **Conexiones** , debajo de **Sitios**, haga clic en en el sitio que hospeda la aplicación web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .  
  
3.  En el panel **Acciones** , haga clic en **Enlaces**.  
  
4.  Haga clic en **Agregar**.  
  
5.  En la lista, seleccione **https**.  
  
6.  Seleccione el certificado SSL.  
  
7.  Haga clic en **Aceptar**.  
  
8.  Opcional. Para quitar HTTP de modo que los usuarios puedan tener acceso al sitio solo con HTTP, en la lista, haga clic en la fila con **http**. Haga clic en **Quitar** y, en el cuadro de diálogo de confirmación, haga clic en **Sí**.  
  
    > [!IMPORTANT]  
    >  Debe cambiar las configuraciones basicHttp y wsHttpBinding después de quitar HTTP.  
  
9. Para cerrar el cuadro de diálogo **Enlaces de sitios** , haga clic en **Cerrar**.  
  
10. Abra ahora el archivo web.config desde *unidad*:\Archivos de programa\Microsoft SQL Server\130\Master Data Services\WebApplication.  
  
11. Busque la cadena `<security mode="Message">` y cámbiela a `<security mode="Transport">`.  

12. Cambie `<serviceMetadata httpGetEnable="true" httpsGetEnabled="false">` por `<serviceMetadata httpGetEnable="false" httpsGetEnabled="true">` para evitar problemas que puedan aparecer en el cliente de Silverlight.

13. Guarde el archivo y ciérrelo. Si obtiene un error, podría deberse a que ha habilitado UAC. Para obtener más información, vea [Desactivar Control de cuentas de usuario](http://technet.microsoft.com/library/cc709691\(WS.10\).aspx). Ahora los usuarios deben poder usar HTTPS para tener acceso al sitio.  

  
## <a name="see-also"></a>Vea también  
 [Crear una aplicación web de Master Data Manager &#40;Master Data Services&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  

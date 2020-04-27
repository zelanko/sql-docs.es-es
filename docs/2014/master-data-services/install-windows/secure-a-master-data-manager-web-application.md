---
title: Proteger una aplicación web de Master Data Manager | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: e360ba3a-e96b-4f85-b588-ed1f767fa973
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2bcbdacd6d08a6139975c20bb8f1d5010195375b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "65479352"
---
# <a name="secure-a-master-data-manager-web-application"></a>Proteger una aplicación web Master Data Services
  Puede proteger la aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] con HTTPS.  
  
> [!NOTE]  
>  La aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] puede usa HTTP o HTTPS, pero no ambos.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar el procedimiento:  
  
-   Debe ser administrador en el servidor web donde está instalado [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .  
  
-   MDS debe estar instalado en el servidor web y debe existir una aplicación web. Para obtener más información, vea [Instalar Master Data Services](install-master-data-services.md) y [Crear una aplicación web de Master Data Manager &#40;Master Data Services&#41;](create-a-master-data-manager-web-application-master-data-services.md).  
  
### <a name="to-secure-the-master-data-manager-web-application-with-https"></a>Para proteger la aplicación web Administrador de datos maestros con HTTP  
  
1.  Después de confirmar que la aplicación web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] está configurada correctamente con HTTP, cree un certificado en IIS. Para obtener más información, vea [Configurar certificados de servidor en IIS 7](https://technet.microsoft.com/library/cc732230\(WS.10\).aspx).  
  
2.  En el panel **Conexiones** , debajo de **Sitios**, haga clic en en el sitio que hospeda la aplicación web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .  
  
3.  En el panel **Acciones**, haga clic en **Enlaces**.  
  
4.  Haga clic en **Agregar**.  
  
5.  En la lista, seleccione **https**.  
  
6.  Seleccione el certificado SSL.  
  
7.  Haga clic en **Aceptar**.  
  
8.  Opcional. Para quitar HTTP de modo que los usuarios puedan tener acceso al sitio solo con HTTP, en la lista, haga clic en la fila con **http**. Haga clic en **Quitar** y, en el cuadro de diálogo de confirmación, haga clic en **Sí**.  
  
    > [!IMPORTANT]  
    >  Debe cambiar las configuraciones basicHttp y wsHttpBinding después de quitar HTTP.  
  
9. Para cerrar el cuadro de diálogo **Enlaces de sitios** , haga clic en **Cerrar**.  
  
10. Abra ahora el archivo web.config desde *drive*:\Archivos de programa\Microsoft SQL Server\120\Master Data Services\WebApplication.  
  
11. Busque la cadena `<security mode="Message">` y cámbiela a `<security mode="Transport">`.  
  
12. Guarde y cierre el archivo. Si obtiene un error, podría deberse a que ha habilitado UAC. Para obtener más información, vea [Desactivar Control de cuentas de usuario](https://technet.microsoft.com/library/cc709691\(WS.10\).aspx). Ahora los usuarios deben poder usar HTTPS para tener acceso al sitio.  
  
## <a name="see-also"></a>Consulte también  
 [Crear una aplicación web de Master Data Manager &#40;Master Data Services&#41;](create-a-master-data-manager-web-application-master-data-services.md)  
  
  

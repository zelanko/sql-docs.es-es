---
title: Instalar Analysis Services | Documentos de Microsoft
ms.custom: 
ms.date: 04/11/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: instances
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cd6ac80d-b735-4e3e-a024-489f1409ad33
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 084223d83c3786610dbce145f27a4c18a6409769
ms.contentlocale: es-es
ms.lasthandoff: 09/27/2017

---
# <a name="install-sql-server-analysis-services"></a>Instalar SQL Server Analysis Services
  SQL Server Analysis Services es un servidor de bases de datos analíticas que hospeda modelos tabulares, cubos multidimensionales y modelos de minería de datos que se pueden acceder desde informes, hojas de cálculo y paneles.  
  
 Analysis Services es varias instancias, lo que significan que puede instalar más de una copia en un único equipo o ejecutar versiones nuevas y antiguas en paralelo. Cualquier instancia que se instale se ejecuta en uno de tres modos, según lo que se determine durante la instalación: multidimensional y de minería de datos, tabular o SharePoint. Si quiere usar varios modos, necesitará una instancia independiente para cada uno.  
  
 Después de instalar el servidor en un modo determinado, puede usarlo para hospedar soluciones conformes con ese modo. Por ejemplo, se necesita un servidor de modo tabular para acceder a los datos de modelo tabulares a través de la red.  
  
## <a name="get-tools-and-designers"></a>Obtener herramientas y diseñadores  
 El programa de instalación de SQL Server ya no instala los diseñadores de modelos ni las herramientas de administración usados para el diseño de soluciones o la administración de servidores. En esta versión, las herramientas tienen un programa de instalación independiente, al que se puede acceder desde los vínculos siguientes:  
  
-   [Descarga de SQL Server Management Studio (SSMS)](../../../ssms/download-sql-server-management-studio-ssms.md)  
  
-   [Descargar SQL Server Data Tools (SSDT)](../../../ssdt/download-sql-server-data-tools-ssdt.md)  
  
 Necesitará SSMS y SSDT para trabajar con datos e instancias de Analysis Services. Herramientas pueden instalarse en cualquier ubicación, pero no olvide configurar puertos en el servidor antes de intentar una conexión. Para obtener información detallada, vea [Configurar Firewall de Windows para permitir el acceso a Analysis Services](../../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md) .  
  
## <a name="install-using-a-wizard"></a>Instalar mediante un asistente  
 La siguiente lista muestra las páginas del Asistente para la instalación de SQL Server que se usan para instalar Analysis Services.  
  
1.  Seleccione **Analysis Services** en el árbol de características del programa de instalación.  
  
     ![Árbol de características del programa de instalación que muestra Analysis Services](../../../analysis-services/instances/install-windows/media/ssas-setupas.gif "árbol de características del programa de instalación que muestra Analysis Services")  
  
2.  En la página de configuración de Analysis Services, seleccione un modo. Modo tabular es el valor predeterminado...  
  
     ![Página de configuración con opciones de configuración de Analysis Services](../../../analysis-services/instances/install-windows/media/ssas-setupasconfig.png "página de configuración con opciones de configuración de Analysis Services")  
  
  El modo tabular utiliza el motor de análisis en memoria xVelocity (VertiPaq), que es el almacenamiento predeterminado para los modelos tabulares. Después de implementar los modelos tabulares en el servidor, puede configurar selectivamente las soluciones tabulares para utilizar el almacenamiento de disco de DirectQuery como una alternativa al almacenamiento de límite de memoria.  
 
 Multidimensional y minería de datos de modo se usa MOLAP como almacenamiento predeterminado para los modelos implementados en Analysis Services. Después de implementar en el servidor, puede configurar una solución para usar ROLAP si quiere ejecutar consultas directamente en la base de datos relacional en lugar de almacenar los datos de la consulta en una base de datos multidimensional de Analysis Services.  
  

  
 La administración de memoria y la configuración de E/S se pueden ajustar para obtener un mejor rendimiento al usar modos de almacenamiento no predeterminados. Vea [Propiedades de servidor en Analysis Services](../../../analysis-services/server-properties/server-properties-in-analysis-services.md) para obtener más información.  
  
## <a name="command-line-setup"></a>Instalación de línea de Comandos  
 El programa de instalación de SQL Server incluye un parámetro (**ASSERVERMODE**) que especifica el modo de servidor. En el siguiente ejemplo se muestra una instalación de la línea de comandos que instala Analysis Services en modo de servidor tabular.  
  
```  
  
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /FEATURES=AS /ASSERVERMODE=TABULAR /INSTANCENAME=ASTabular /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
 **INSTANCENAME** debe tener menos de 17 caracteres.  
  
 Todos los valores de cuenta de marcador de posición se deben reemplazar con cuentas y contraseñas válidas.  
  
 **ASSERVERMODE** distingue entre mayúsculas y minúsculas.  Todos los valores se deben expresar en mayúsculas. En la tabla siguiente se describen los valores válidos de **ASSERVERMODE**.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|TABULAR|Es el valor predeterminado. Si no establece **ASSERVERMODE**, el servidor está instalado en modo Tabular.|
|MULTIDIMENSIONAL|Este valor es opcional.|  
|POWERPIVOT|Este valor es opcional. En ejercicio, si establece el parámetro **ROLE** , el modo de servidor se establece automáticamente en 1, haciendo que **ASSERVERMODE** sea opcional en una instalación de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint. Para obtener más información, consulte [Instalar Power Pivot desde el símbolo del sistema](http://msdn.microsoft.com/en-us/7f1f2b28-c9f5-49ad-934b-02f2fa6b9328).|  
  
  
## <a name="see-also"></a>Vea también  
 [Determinar el modo de servidor de una instancia de Analysis Services](../../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [Creación de modelos tabular (SSAS Tabular)](https://msdn.microsoft.com/library/hh212945(v=sql.110).aspx)  
  
  


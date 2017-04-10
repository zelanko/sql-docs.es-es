---
title: "Instalar Analysis Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cd6ac80d-b735-4e3e-a024-489f1409ad33
caps.latest.revision: 20
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 19
---
# Instalar Analysis Services
  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] es un servidor de bases de datos analíticas que hospeda modelos tabulares, cubos multidimensionales y modelos de minería de datos a los que se puede acceder desde informes, hojas de cálculo y paneles.  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] es de varias instancias, lo que significa que es posible instalar más de una copia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en un único equipo o ejecutar versiones nuevas y antiguas en paralelo. Cualquier instancia que se instale se ejecuta en uno de tres modos, según lo que se determine durante la instalación: multidimensional y de minería de datos, tabular o SharePoint. Si quiere usar varios modos, necesitará una instancia independiente para cada uno.  
  
 Después de instalar el servidor en un modo determinado, puede usarlo para hospedar soluciones conformes con ese modo. Por ejemplo, se necesita un servidor de modo tabular para acceder a los datos de modelo tabulares a través de la red.  
  
## Obtener herramientas y diseñadores  
 El programa de instalación de SQL Server ya no instala los diseñadores de modelos ni las herramientas de administración usados para el diseño de soluciones o la administración de servidores. En esta versión, las herramientas tienen un programa de instalación independiente, al que se puede acceder desde los vínculos siguientes:  
  
-   [Descargar SQL Server Management Studio para SQL Server 2016](https://msdn.microsoft.com/en-US/library/mt238290.aspx)  
  
-   [Descargar SQL Server Data Tools para SQL Server 2016](https://msdn.microsoft.com/en-US/library/mt204009.aspx)  
  
 Necesitará Management Studio y SQL Server Data Tools para trabajar con datos e instancias de Analysis Services. Las herramientas pueden instalarse en cualquier ubicación, pero asegúrese de configurar puertos en el servidor antes de intentar una conexión. Para obtener información detallada, vea [Configure the Windows Firewall to Allow Analysis Services Access](../../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md) .  
  
## Instalar mediante un asistente  
 La siguiente lista muestra las páginas del Asistente para la instalación de SQL Server que se usan para instalar Analysis Services.  
  
1.  Seleccione **Analysis Services** en el árbol de características del programa de instalación.  
  
     ![Setup feature tree showing Analsyis Services](../../../analysis-services/instances/install-windows/media/ssas-setupas.gif "Setup feature tree showing Analsyis Services")  
  
2.  Si quiere una instancia tabular, en la página Configuración de Analysis Services, asegúrese de seleccionar **Modo tabular** . De lo contrario, el valor predeterminado es **Modo multidimensional y de minería de datos**.  
  
     ![Setup page with Analysis Services config options](../../../analysis-services/instances/install-windows/media/ssas-setupasconfig.png "Setup page with Analysis Services config options")  
  
 El modo multidimensional y de minería de datos usa MOLAP como almacenamiento predeterminado para los modelos implementados en Analysis Services. Después de implementar en el servidor, puede configurar una solución para usar ROLAP si quiere ejecutar consultas directamente en la base de datos relacional en lugar de almacenar los datos de la consulta en una base de datos multidimensional de Analysis Services.  
  
 El modo tabular utiliza el motor analítico en memoria xVelocity (VertiPaq), que es el almacenamiento predeterminado para los modelos tabulares que se implementan en Analysis Services. Después de implementar las soluciones de modelo tabular en el servidor, puede configurar selectivamente las soluciones tabulares para utilizar el almacenamiento en disco de DirectQuery como una alternativa al almacenamiento enlazado a la memoria.  
  
 La administración de memoria y la configuración de E/S se pueden ajustar para obtener un mejor rendimiento al usar modos de almacenamiento no predeterminados. Vea [Propiedades de servidor en Analysis Services](../../../analysis-services/server-properties/server-properties-in-analysis-services.md) para obtener más información.  
  
## Instalación de línea de Comandos  
 El programa de instalación de SQL Server incluye un parámetro (**ASSERVERMODE**) que especifica el modo de servidor. En el siguiente ejemplo se muestra una instalación de la línea de comandos que instala Analysis Services en modo de servidor tabular.  
  
```  
  
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /FEATURES=AS /ASSERVERMODE=TABULAR /INSTANCENAME=ASTabular /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
 **INSTANCENAME** debe tener menos de 17 caracteres.  
  
 Todos los valores de cuenta de marcador de posición se deben reemplazar con cuentas y contraseñas válidas.  
  
 **ASSERVERMODE** distingue entre mayúsculas y minúsculas.  Todos los valores se deben expresar en mayúsculas. En la tabla siguiente se describen los valores válidos de **ASSERVERMODE**.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|MULTIDIMENSIONAL|Es el valor predeterminado. Si no establece **ASSERVERMODE**, el servidor se instala en modo de servidor multidimensional.|  
|POWERPIVOT|Este valor es opcional. En ejercicio, si establece el parámetro **ROLE**, el modo de servidor se establece automáticamente en 1, haciendo que **ASSERVERMODE** sea opcional en una instalación de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint. Para obtener más información, consulte [Instalar Power Pivot desde el símbolo del sistema](http://msdn.microsoft.com/es-es/7f1f2b28-c9f5-49ad-934b-02f2fa6b9328).|  
|TABULAR|Se requiere este valor si va a instalar Analysis Services en modo tabular utilizando la instalación de la línea de comandos.|  
  
## Vea también  
 [Determinar el modo de servidor de una instancia de Analysis Services](../../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [Conversión de una base de datos tabular en memoria a DirectQuery en SQL Server Management Studio &#40;SSMS&#41;](../Topic/Convert%20an%20in-memory%20Tabular%20Database%20to%20DirectQuery%20in%20SQL%20Server%20Management%20Studio%20\(SSMS\).md)   
 [Modelos tabulares &#40;SSAS&#41;](../Topic/Tabular%20Modeling%20\(SSAS\).md)  
  
  
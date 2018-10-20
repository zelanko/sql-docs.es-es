---
title: Costes y topologías de licencia de ejemplo de inteligencia empresarial de autoasistencia de SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 682b8711-407a-48d1-9807-415d4c24dad6
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: a7e08f483f1f56dcab49391190fd1c6edc11f6db
ms.sourcegitcommit: 3cd6068f3baf434a4a8074ba67223899e77a690b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2018
ms.locfileid: "49462061"
---
# <a name="example-license-topologies-and-costs--for-sql-server-2014-self-service-business-intelligence"></a>Ejemplos de topologías y costos de licencias para Business Intelligence de autoservicio de SQL Server 2014
  En este tema se indican las consideraciones de alto nivel para seleccionar la edición Business Intelligence de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o la edición Enterprise de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El tema incluye varios ejemplos de topologías locales de Business Intelligence (BI) de autoservicio de Microsoft. Los ejemplos incluyen las ediciones y las licencias que puede utilizar para optimizar el equilibrio entre el costo y el rendimiento. Las topologías, el número de servidores y el costo de las licencias se ofrecen **solo a modo de ejemplo**. Con Microsoft [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y Microsoft SharePoint 2013 se introdujeron varios cambios en la estructura de licencias que proporcionan más opciones para obtener licencias para servidores, usuarios y dispositivos. Las licencias de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] admiten los mismos escenarios de Business Intelligence.  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] está disponible en la edición Business Intelligence y ofrece licencias por núcleo para algunas ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Con SharePoint 2013 se simplificaron las licencias de SharePoint Server para escenarios de extranet e Internet, así como las opciones para SharePoint Online.  
  
 Antes realizar la compra, visite la sección “Cómo comprar” de cada producto y consulte sus requisitos específicos en cuanto a licencias a su representante o distribuidor local de Microsoft. Para obtener información sobre los planes y costos de licencias más recientes, vea lo siguiente:  
  
-   [Acerca de las licencias – SQL Server 2014](http://www.microsoft.com/licensing/about-licensing/sql2014.aspx)  
  
-   [Licencias de SharePoint 2013](http://office.microsoft.com/sharepoint/sharepoint-licensing-overview-collaboration-software-FX103789438.aspx).  
  
 **En este tema:**  
  
-   [Componentes de SQL Server Business Intelligence](#bkmk_bi_components)  
  
-   [Resumen de licencias de SQL Server 2014](#bkmk_sql_server_license)  
  
-   [Resumen de licencias de SharePoint 2013](#bkmk_sharepoint_license)  
  
-   [Topología de 3 niveles con servidores PowerPivot independientes](#bkmk_3tier_powerpivot)  
  
-   [Topología de 3 niveles](#bkmk_3tier)  
  
-   [Topología de 2 niveles](#bkmk_2tier)  
  
-   [Contenido de referencia y la Comunidad](#bkmk_reference)  
  
##  <a name="bkmk_bi_components"></a> Componentes de SQL Server Business Intelligence  
 Este tema se centra en las tecnologías de servidor de SQL Server y de SharePoint. Los costos y los ejemplos no indican específicamente los componentes de Microsoft Windows Server o Microsoft Office necesarios para una solución completa de cliente y servidor. Los componentes de SQL Server Business Intelligence de los que trata este tema son SQL Server Reporting Services que se ejecuta en modo de SharePoint y PowerPivot para SharePoint. Los componentes incluyen las características siguientes:  
  
-   Libros PowerPivot interactivos en el explorador.  
  
-   Informes de [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] interactivos en SharePoint.  
  
-   Galería de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], Actualización de datos programada, Panel de administración.  
  
-   Reporting Services en modo de SharePoint, incluyendo las alertas de datos.  
  
 Para obtener más información, vea la tabla de características de [instalar características de BI de SQL Server con SharePoint &#40;PowerPivot y Reporting Services&#41;](../../../2014/sql-server/install/install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md).  
  
## <a name="license-summary"></a>Resumen de licencias  
 En esta sección se resumen los requisitos de licencias para SQL Server y SharePoint. La información es un resumen de alto nivel y solo cubre los escenarios utilizadas en los diagramas de topología y los ejemplos de costo de este documento. Vea los vínculos de contenido indicados para obtener información más detallada sobre las licencias. Los precios de ejemplo se basan en los precios del Programa Microsoft Open License (MOLP).  
  
 Una práctica habitual consiste en utilizar **Enterprise Edition** para los servidores que ejecutan el motor de base de datos de SQL Server y **Business Intelligence Edition** para los servidores que ejecutan Reporting Services o PowerPivot para SharePoint. Sin embargo, factores como el **número de usuarios** y el **número de núcleos de servidor** de la implementación afectan al costo y a la decisión sobre qué edición utilizar.  
  
###  <a name="bkmk_sql_server_license"></a> Resumen de licencias de SQL Server 2014  
  
-   SQL Server Enterprise Edition utiliza licencias basadas en núcleo. Las licencias basadas en núcleo se venden en paquetes de **dos núcleos** .  
  
-   La edición SQL Server BI utiliza licencias de servidor y licencias de acceso de cliente (CAL).  
  
-   Las licencias CAL se basan en cada usuario o dispositivo conectado a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], independientemente del número de servidores a los que se conecten.  
  
-   Las licencias basadas en núcleo requieren que todos los núcleos del servidor dispongan de una licencia. Para cada procesador físico del servidor se necesita un mínimo de **cuatro** licencias basadas en núcleo.  
  
 En la tabla siguiente se resumen los detalles de las licencias utilizadas para el diseño de la implementación y la estimación de costo de las licencias. **NOTA:**  el precio se muestra únicamente con fines demostrativos.  
  
|Ediciones de SQL Server|Licencia de SQL Server + Licencia de acceso de cliente (CAL)|Licencia basada en núcleo de SQL Server|  
|-------------------------|---------------------------------------------------------|-----------------------------------|  
|Enterprise|No aplicable|**(Sí)** $6874 X [n.º de núcleos] X [factor de núcleo]|  
|Business Intelligence|**(Sí)** $8592 + $199 por CAL|No aplicable|  
|Estándar|**(Sí)**|**(Sí)**|  
  
 Para obtener más información acerca de los precios de las licencias de ejemplo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vea:  
  
-   [Concesión de licencias para entornos virtuales](http://www.microsoft.com/licensing/about-licensing/virtualization.aspx) (http://www.microsoft.com/licensing/about-licensing/virtualization.aspx).  
  
-   [SQL Server 2014 licencias de hoja de datos - página principal de Microsoft](http://download.microsoft.com/download/6/6/F/66FF3259-1466-4BBA-A505-2E3DA5B2B1FA/SQL_Server_2014_Licensing_Datasheet.pdf) (http://download.microsoft.com/download/6/6/F/66FF3259-1466-4BBA-A505-2E3DA5B2B1FA/SQL_Server_2014_Licensing_Datasheet.pdf).  
  
-   [Ediciones de SQL server 2014 y licencias](http://www.microsoft.com/licensing/about-licensing/sql2014.aspx#tab=2)  
  
1.  **Suposiciones sobre SQL Server y más información de licencia:**  
  
2.  Los diagramas de este tema usan la edición Enterprise de SQL Server para los servidores de bases de datos, de modo que esté disponible el conjunto completo de características de alta disponibilidad, como los grupos de disponibilidad AlwaysOn. Para obtener más información, vea [Features Supported by the Editions of SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
3.  Todos los servidores de este ejemplo contienen 2 procesadores Intel Xeon de 6 núcleos, por lo que se usa un **factor de núcleo de SQL Server** de **1** al calcular los costos de las licencias. Para obtener más información sobre los factores de núcleo y los costos de licencia, consulte [tabla de Factor de núcleo de SQL Server](http://download.microsoft.com/download/9/B/F/9BF63163-D8F9-4339-90AA-EBC9AAFC49AD/SQL2012_CoreFactorTable_Mar2012.pdf) (http://download.microsoft.com/download/0/C/8/0C85665B-11EA-4FF5-B37C-8CC21CF95AC4/BizTalk%202013_CoreFactorTable_**3.19.2013**. v4.pdf).  
  
###  <a name="bkmk_sharepoint_license"></a> Resumen de licencias de SharePoint 2013  
 En la lista siguiente se resume el modelo de licencias utilizado para el diseño de la implementación y la estimación de costo de las licencias. el precio se muestra únicamente con fines demostrativos.  
  
1.  Se necesita una licencia de servidor de SharePoint para cada instancia de Microsoft SharePoint Server.  
  
2.  Para asignar licencias de SharePoint Enterprise, para cada usuario final o dispositivo final compre una **licencia CAL Standard** de Microsoft SharePoint Server 2013 además de una **licencia CAL Enterprise**de Microsoft SharePoint Server 2013.  
  
3.  Se debe comprar una licencia CAL de SharePoint por cada usuario o dispositivo que tiene acceso a los servidores de SharePoint. No es necesario comprar licencias CAL para cada servidor.  
  
 Por ejemplo, si el entorno consta de 2 instancias que utilizan 100 usuarios, y los costos que le presupuestaron fueron estos:  
  
-   Licencia CAL Standard de Microsoft SharePoint Server 2013: **$107.99**  
  
-   Licencia CAL Enterprise de Microsoft SharePoint Server 2013: **$94.99**  
  
-   Licencia de Microsoft SharePoint Server 2013: **$6,412.99**  
  
 El costo sería: **$33,123.98**  
  
-   Licencia CAL: ($107.99 +$94.99) X 100) =$20,298.00  
  
-   Licencia de servidor: ($6,412.99 X 2) =$12,825.98  
  
 **Suposiciones sobre SharePoint y más información de licencia:**  
  
 Las implementaciones de ejemplo son todas entornos de intranet, por lo que es necesaria la licencia CAL de SharePoint.  
  
-   [La lista completa de licencias de SharePoint](http://technet.microsoft.com/library/jj819267.aspx#bkmk_FeaturesOnPremise) (http://technet.microsoft.com/library/jj819267.aspx#bkmk_FeaturesOnPremise).  
  
-   [Cómo comprar SharePoint](http://sharepoint.microsoft.com/Pages/buy.aspx) (http://sharepoint.microsoft.com/Pages/buy.aspx).  
  
##  <a name="bkmk_3tier_powerpivot"></a> Topología con independiente de 3 niveles [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] servidores  
 En este ejemplo se muestra que, con 800 usuarios o menos, resulta más económico usar la edición SQL Server BI para los servidores de aplicaciones de SharePoint y los servidores [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. Sin embargo, cuando hay 800 usuarios o más, SQL Server Enterprise Edition resulta más económico. Las licencias basadas en núcleo son independientes del número de usuarios, por lo que hay un punto de umbral de costo en el que se comparan los costos de licencias CAL y de núcleo, y el número de las de los usuarios aumenta. A partir del punto de umbral, la edición Enterprise es la solución más económica. Para determinar el umbral de costo, compare los costos basándose en el número de núcleos para los que necesita licencias con el número de licencias CAL de dispositivo final o de usuario que necesite.  
  
-   Este ejemplo es una implementación en intranet, por lo que las licencias CAL de SharePoint se aplican a SharePoint 2013.  
  
-   El rol de aplicación (2) incluye SQL Server Reporting Services instalado en modo de SharePoint.  
  
     Las bases de datos de la aplicación de servicio de SharePoint se ejecutan en servidores con rol de base de datos (4).  
  
-   [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint se ejecuta en servidores independientes (3). [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint 2013 se ejecuta fuera de la granja de SharePoint y se puede instalar en servidores que no incluyen una instalación de SharePoint, mejorar el rendimiento.  
  
-   El rol de base de datos (4) utiliza SQL Server Enterprise, por lo que la característica grupos de disponibilidad AlwaysOn de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está disponible.  
  
 ![bi_license_3tiers_and_ASseparate](../../../2014/sql-server/install/media/bi-license-3tiers-and-asseparate.gif "bi_license_3tiers_and_ASseparate")  
  
 Con 100 usuarios, la edición SQL Server BI es más económica.  
  
 ![bi_license_3tiers_and_ASseperate_calcs](../../../2014/sql-server/install/media/bi-license-3tiers-and-asseperate-calcs.gif "bi_license_3tiers_and_ASseperate_calcs")  
  
 Sin embargo, con 300 usuarios resulta más económico usar SQL Server Enterprise Edition.  
  
 ![bi_license_3tiers_and_ASseperate_calcs2](../../../2014/sql-server/install/media/bi-license-3tiers-and-asseperate-calcs2.gif "bi_license_3tiers_and_ASseperate_calcs2")  
  
##  <a name="bkmk_3tier"></a> Topología de 3 niveles  
 En este ejemplo se muestra que con 100 usuarios o menos, resulta más económico utilizar la edición SQL BI para los servidores que ejecutan la funcionalidad BI de SQL Server. Sin embargo, cuando hay 500 usuarios o más, SQL Server Enterprise Edition resulta más económico.  
  
-   Este ejemplo es una implementación en intranet, por lo que las licencias CAL de SharePoint se aplican a SharePoint 2013.  
  
-   Analysis Services en modo PowerPivot (2) se ejecuta fuera de la granja, pero PowerPivot se ejecuta **en los mismos servidores físicos** con el otro rol de aplicación.  
  
-   El rol de base de datos (3) utiliza SQL Server Enterprise, por lo que la característica grupos de disponibilidad AlwaysOn de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está disponible.  
  
 ![bi_license_3tiers](../../../2014/sql-server/install/media/bi-license-3tiers.gif "bi_license_3tiers")  
  
 Con 100 usuarios, la edición SQL Server BI es más económica.  
  
 ![bi_license_3tiers_calcs1](../../../2014/sql-server/install/media/bi-license-3tiers-calcs1.gif "bi_license_3tiers_calcs1")  
  
 Sin embargo, con 500 usuarios resulta más económico usar SQL Server Enterprise Edition.  
  
 ![bi_license_3tiers_calcs3](../../../2014/sql-server/install/media/bi-license-3tiers-calcs3.gif "bi_license_3tiers_calcs3")  
  
##  <a name="bkmk_2tier"></a> Topología de 2 niveles  
 Con solo 2 niveles, se utiliza SQL Server Enterprise Edition de modo que la característica grupos de disponibilidad AlwaysOn de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esté disponible para el motor de base de datos de SQL Server. Por consiguiente, no existen diferencias de costos que comparar entre las ediciones de SQL Server. La única variable es el costo de las licencias CAL de SharePoint basado en el número de usuarios.  
  
-   Este ejemplo es una implementación en intranet, por lo que las licencias CAL de SharePoint se aplican a SharePoint 2013.  
  
-   Analysis Services en modo PowerPivot se ejecuta fuera de la granja, pero PowerPivot se ejecuta en los mismos servidores físicos (2) que el motor de base de datos de SQL Server.  
  
 ![bi_license_2tiers](../../../2014/sql-server/install/media/bi-license-2tiers.gif "bi_license_2tiers")  
  
 ![bi_license_2tiers_calcs1](../../../2014/sql-server/install/media/bi-license-2tiers-calcs1.gif "bi_license_2tiers_calcs1")  
  
##  <a name="bkmk_reference"></a> Contenido de referencia y la Comunidad  
  
### <a name="license-tools"></a>Herramientas de licencias  
  
-   [Microsoft License Advisor](http://mla.microsoft.com/default.aspx) (http://mla.microsoft.com/default.aspx).  
  
-   [Herramienta de decisión (CAL) de la licencia de acceso de cliente](http://www.microsoft.com/licensing/CalTool/) (http://www.microsoft.com/licensing/CalTool/).  
  
-   [Centro de negocios de Microsoft: Cómo comprar](http://www.microsoftbusinesshub.com/How_To_Buy#) (http://www.microsoftbusinesshub.com/How_To_Buy#).  
  
### <a name="microsoft-license-information"></a>Información sobre licencias de Microsoft  
  
-   [Acerca de las licencias: Licencias de acceso de cliente y licencias de administración](http://www.microsoft.com/licensing/about-licensing/client-access-license.aspx) (http://www.microsoft.com/licensing/about-licensing/client-access-license.aspx).  
  
-   [Acerca de las licencias: Búsqueda de licencias de producto](http://www.microsoftvolumelicensing.com/default.aspx) (http://www.microsoftvolumelicensing.com/default.aspx).  
  
-   [Licencias por volumen: precios y cómo comprar](http://www.microsoft.com/licensing/how-to-buy/how-to-buy.aspx) (http://www.microsoft.com/licensing/how-to-buy/how-to-buy.aspx).  
  
### <a name="community-content"></a>Contenido de la comunidad  
  
-   [Licencias de SQL Server 2014 Developer Edition](http://sqlmag.com/sql-server-2014/sql-server-2014-developer-edition-licensing).  
  
-   [Cambios de licencias de SQL Server 2014](http://www.brentozar.com/archive/2014/04/sql-server-2014-licensing-changes)(http://www.brentozar.com/archive/2014/04/sql-server-2014-licensing-changes).  
  
-   [Cambios de licencia para SQL Server 2014](https://www.directionsonmicrosoft.com/sites/default/files/PDFs/Licensing_Changes_for_SQL_Server_2014.pdf)(https://www.directionsonmicrosoft.com/sites/default/files/PDFs/Licensing_Changes_for_SQL_Server_2014.pdf).  
  
-   [Estimar los costos de licencias de SharePoint 2013](http://www.degdigital.com/blog/sharepoint-2013-licensing-for-dummies/) (http://www.degdigital.com/blog/sharepoint-2013-licensing-for-dummies/).  
  
-   [Comunidad de clientes de licencias por volumen](http://www.microsoft.com/licensing/existing-customers/community.aspx) (http://www.microsoft.com/licensing/existing-customers/community.aspx).  
  
  

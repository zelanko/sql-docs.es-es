---
title: Restaurar desde Power Pivot | Documentos de Microsoft
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql11.asvs.ssmsimbi.RestoreFromPP.f1
ms.assetid: 232ac8ed-77fe-47d8-acd3-59bc2fdfdf48
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a35f1ddb32a5adf8e422154fea0a56feb1010061
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="restore-from-power-pivot"></a>Restaurar de Power Pivot
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Puede usar la característica Restaurar de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en SQL Server Management Studio para crear una base de datos de modelo tabular en una instancia de Analysis Services (que se ejecute en modo tabular) o para realizar una restauración en una base de datos existente desde un libro de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] (.xlsx).  
  
> [!NOTE]  
>  La plantilla de proyecto Importar de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en SQL Server Data Tools proporciona una funcionalidad similar. Para obtener más información, consulte [importación desde PowerPivot](../../analysis-services/tabular-models/import-from-power-pivot-ssas-tabular.md).  
  
 Cuando use Restaurar de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], tenga en cuenta lo siguiente:  
  
-   Para poder usa Restaurar de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], debe haber iniciado una sesión como miembro del rol Administradores de servidor en la instancia de Analysis Services.  
  
-   La cuenta de servicio de la instancia de Analysis Services debe tener permisos de lectura en el archivo de libro desde el que va a restaurar.  
  
-   De forma predeterminada, cuando se restaura una base de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], la propiedad Información de suplantación de origen de datos de la base de datos de modelo tabular se establece en Valor predeterminado, que especifica la cuenta de servicio de la instancia de Analysis Services. Se recomienda cambiar las credenciales de suplantación a una cuenta de usuario de Windows en Propiedades de la base de datos. Para obtener más información, consulte [suplantación](../../analysis-services/tabular-models/impersonation-ssas-tabular.md).  
  
-   Los datos del modelo de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] se copiarán en una base de datos de modelo tabular nueva o existente en la instancia de Analysis Services. Si el libro de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] contiene tablas vinculadas, se volverán a crear como una tabla sin un origen de datos, de manera similar a una tabla creada mediante Pegar en nueva tabla.  
  
### <a name="to-restore-from-power-pivot"></a>Para restaurar desde Power Pivot  
  
1.  En SSMS, en la instancia de Active Directory donde quiera realizar la restauración, haga clic con el botón derecho en **Bases de datos** y, después, haga clic en **Restaurar desde [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**.  
  
2.  En el cuadro de diálogo **Restaurar desde [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**, en **Restaurar origen**, en **Archivo de copia de seguridad**, haga clic en **Examinar** y seleccione un archivo .abf o .xslx desde el que va a realizar la restauración.  
  
3.  En **Restaurar destino**, en **Restaurar base de datos**, escriba un nombre para una base de datos nueva o para una base de datos existente. Si no especifica ningún nombre, se usa el nombre del libro.  
  
4.  En **Ubicación de almacenamiento**, haga clic en **Examinar**y seleccione una ubicación para almacenar la base de datos.  
  
5.  En **Opciones**, deje activada **Incluir información de seguridad** . Cuando la restauración se realiza desde un libro de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , este valor no se aplica.  
  
## <a name="see-also"></a>Vea también  
 [Bases de datos de modelo tabular](../../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md)   
 [Importación desde Power Pivot](../../analysis-services/tabular-models/import-from-power-pivot-ssas-tabular.md)  
  
  

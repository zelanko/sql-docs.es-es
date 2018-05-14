---
title: Restaurar desde Power Pivot | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f95c1e891a218af73eb7c5bacbd1ea5a48e3a830
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
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
  
  

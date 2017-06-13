---
title: "Crear un componente de tiempo de diseño de elemento de informe personalizado | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom report items, creating
ms.assetid: 323fd58a-a462-4c48-b188-77ebc0b4212e
caps.latest.revision: 37
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 2cb994a0cb4dde6b6ea5f671238272e574e7721b
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="creating-a-custom-report-item-design-time-component"></a>Crear un componente de tiempo de diseño de elemento de informe personalizado
  Un componente de tiempo de diseño de elemento de informe personalizado es un control que se puede utilizar en el entorno de Visual Studio Report Designer. El componente de tiempo de diseño de elemento de informe personalizado proporciona una superficie de diseño activada que puede aceptar las operaciones de arrastrar y colocar, la integración con el explorador de propiedades de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], y la capacidad de proporcionar los editores de propiedades personalizados.  
  
 Con un componente de tiempo de diseño de elemento de informe personalizado, el usuario puede colocar un elemento de informe personalizado en un informe en el entorno de diseño, establecer las propiedades de datos personalizadas en el elemento de informe personalizado y, a continuación, guardar el elemento de informe personalizado como parte del proyecto de informe.  
  
 Las propiedades que se establecen utilizando el componente de tiempo de diseño en el entorno de desarrollo se serializan y deserializan por el entorno de diseño del host y, a continuación, se guardan como elementos en el archivo de lenguaje RDL (Report Definition Language). Cuando el procesador de informes ejecuta el informe, pasa las propiedades que están establecidas utilizando el componente de tiempo de diseño a un componente de tiempo de ejecución del elemento de informe personalizado, que representa el elemento de informe personalizado y lo devuelve al procesador de informes.  
  
> [!NOTE]  
>  El componente de tiempo de diseño de elemento de informe personalizado se implementa como un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] componente. En este documento se describirán los detalles de la implementación específicos al componente de tiempo de diseño del elemento de informe personalizado. Para obtener más información sobre cómo desarrollar componentes mediante la [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], consulte [componentes en Visual Studio](http://go.microsoft.com/fwlink/?LinkId=116576) en MSDN library.  
  
 Para obtener un ejemplo de un elemento de informe personalizado implementado totalmente, vea [muestras de producto de SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="implementing-a-design-time-component"></a>Implementar un componente de tiempo de diseño  
 La clase principal de un componente de tiempo de diseño de elemento de informe personalizado se hereda de la **Microsoft.ReportDesigner.CustomReportItemDesigner** clase. Además de los atributos estándares utilizados para un [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] (control), debe definir la clase de componente un **CustomReportItem** atributo. Este atributo debe corresponder al nombre del elemento de informe personalizado como se define en el archivo reportserver.config. Para obtener una lista de atributos [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], vea Atributos en la documentación de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
 El ejemplo de código siguiente muestra atributos que se aplican a un control de tiempo de diseño del elemento de informe personalizado:  
  
```csharp  
namespace PolygonsCRI  
{  
    [LocalizedName("Polygons")]  
    [Editor(typeof(CustomEditor), typeof(ComponentEditor))]  
        [ToolboxBitmap(typeof(PolygonsDesigner),"Polygons.ico")]  
        [CustomReportItem("Polygons")]  
  
    public class PolygonsDesigner : CustomReportItemDesigner  
    {  
...  
```  
  
### <a name="initializing-the-component"></a>Inicializar el componente  
 Las propiedades especificadas por el usuario para un elemento de informe personalizado se pasan utilizando una clase <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData>. La implementación de la **CustomReportItemDesigner** clase debe reemplazar el **InitializeNewComponent** método para crear una nueva instancia de su componente <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData> clase y establézcalo en valores predeterminados.  
  
 En el ejemplo de código siguiente se muestra un ejemplo de un componente de tiempo de diseño de elemento de informe personalizado durante la invalidación del clase la **CustomReportItemDesigner.InitializeNewComponent** método para inicializar el componente <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData> clase:  
  
```csharp  
public override void InitializeNewComponent()  
        {  
            CustomData = new CustomData();  
            CustomData.DataRowHierarchy = new DataHierarchy();  
  
            // Shape grouping  
            CustomData.DataRowHierarchy.DataMembers.Add(new DataMember());  
            CustomData.DataRowHierarchy.DataMembers[0].Group = new Group();  
            CustomData.DataRowHierarchy.DataMembers[0].Group.Name = Name + "_Shape";  
            CustomData.DataRowHierarchy.DataMembers[0].Group.GroupExpressions.Add(new ReportExpression());  
  
            // Point grouping  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers.Add(new DataMember());  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers[0].Group = new Group();  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers[0].Group.Name = Name + "_Point";  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers[0].Group.GroupExpressions.Add(new ReportExpression());  
  
            // Static column  
            CustomData.DataColumnHierarchy = new DataHierarchy();  
            CustomData.DataColumnHierarchy.DataMembers.Add(new DataMember());  
  
            // Points  
            IList<IList<DataValue>> dataValues = new List<IList<DataValue>>();  
            CustomData.DataRows.Add(dataValues);  
            CustomData.DataRows[0].Add(new List<DataValue>());  
            CustomData.DataRows[0][0].Add(NewDataValue("X", ""));  
            CustomData.DataRows[0][0].Add(NewDataValue("Y", ""));  
        }  
```  
  
### <a name="modifying-component-properties"></a>Modificar propiedades de componentes  
 Puede modificar **CustomData** propiedades en el entorno de diseño de varias maneras. Puede modificar cualquier propiedad que expuesta por el componente de tiempo de diseño que esté marcada con el atributo <xref:System.ComponentModel.BrowsableAttribute> utilizando el explorador de propiedades de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Además, puede modificar las propiedades arrastrando elementos en la superficie de diseño del elemento de informe personalizado o haciendo clic en el control en el entorno de diseño y seleccionando **propiedades** en el menú contextual para mostrar una ventana de propiedades personalizadas.  
  
 El siguiente ejemplo de código muestra un **Microsoft.ReportDesigner.CustomReportItemDesigner.CustomData** propiedad que tiene el <xref:System.ComponentModel.BrowsableAttribute> atributo aplicado:  
  
```csharp  
[Browsable(true), Category("Data")]  
public string DataSetName  
{  
      get  
      {  
         return CustomData.DataSetName;  
      }  
      set  
      {  
         CustomData.DataSetName = value;  
      }  
   }  
  
```  
  
 Puede proporcionar un cuadro de diálogo de editor de propiedades personalizado al componente de tiempo de diseño. La implementación personalizada del editor de propiedades debería heredar de la clase <xref:System.ComponentModel.ComponentEditor> y debería crear una instancia de un cuadro de diálogo que se puede utilizar para la edición de propiedad.  
  
 En el ejemplo siguiente se muestra una implementación de una clase que hereda de <xref:System.ComponentModel.ComponentEditor> y muestra un cuadro de diálogo de editor de propiedades personalizado:  
  
```csharp  
internal sealed class CustomEditor : ComponentEditor  
{  
   public override bool EditComponent(  
      ITypeDescriptorContext context, object component)  
    {  
     PolygonsDesigner designer = (PolygonsDesigner)component;  
     PolygonProperties dialog = new PolygonProperties();  
     dialog.m_designerComponent = designer;  
     DialogResult result = dialog.ShowDialog();  
     if (result == DialogResult.OK)  
     {  
        designer.Invalidate();  
        designer.ChangeService().OnComponentChanged(designer, null, null, null);  
        return true;  
     }  
     else  
        return false;  
    }  
}  
```  
  
 El cuadro de diálogo de editor de propiedades personalizado puede invocar al editor de expresiones del diseñador de informes. En el ejemplo siguiente, el editor de expresiones se invoca cuando el usuario selecciona el primer elemento del cuadro combinado:  
  
```csharp  
private void EditableCombo_SelectedIndexChanged(object sender,   
    EventArgs e)  
{  
   ComboBox combo = (ComboBox)sender;  
   if (combo.SelectedIndex == 0 && m_launchEditor)  
   {  
      m_launchEditor = false;  
      ExpressionEditor editor = new ExpressionEditor();  
      string newValue;  
      newValue = (string)editor.EditValue(null, m_designerComponent.Site, m_oldComboValue);  
      combo.Items[0] = newValue;  
   }  
}  
  
```  
  
### <a name="using-designer-verbs"></a>Utilizar los verbos de diseñador  
 Un verbo de diseñador es un comando de menú vinculado a un controlador de eventos. Puede agregar verbos de diseñador que aparecerán en el menú contextual de un componente cuando el control de tiempo de ejecución del elemento de informe personalizado se utiliza en el entorno de diseño. Puede devolver la lista de verbos de diseñador disponibles desde el componente de tiempo de ejecución mediante la **verbos** propiedad.  
  
 El ejemplo de código siguiente muestra un verbo de diseñador y un controlador de eventos agregados a <xref:System.ComponentModel.Design.DesignerVerbCollection>, así como el código de controlador de eventos:  
  
```csharp  
public override DesignerVerbCollection Verbs  
{  
    get  
    {  
        if (m_verbs == null)  
        {  
            m_verbs = new DesignerVerbCollection();  
            m_verbs.Add(new DesignerVerb("Proportional Scaling", new EventHandler(OnProportionalScaling)));  
         m_verbs[0].Checked = (GetCustomProperty("poly:Proportional") == bool.TrueString);  
        }  
  
        return m_verbs;  
    }  
}  
  
private void OnProportionalScaling(object sender, EventArgs e)  
{  
   bool proportional = !  
        (GetCustomProperty("poly:Proportional") == bool.TrueString);  
   m_verbs[0].Checked = proportional;  
   SetCustomProperty("poly:Proportional", proportional.ToString());  
   ChangeService().OnComponentChanged(this, null, null, null);  
   Invalidate();  
}  
```  
  
### <a name="using-adornments"></a>Utilizar las opciones gráficas  
 Clases de elemento de informe personalizado también pueden implementar un **Microsoft.ReportDesigner.Design.Adornment** clase. Una opción gráfica permite al control de elemento de informe personalizado proporcionar las áreas fuera del rectángulo principal de la superficie de diseño. Estas áreas pueden administrar los eventos de interfaz de usuario, como los clics del mouse y las operaciones de arrastrar y colocar. El **elementos gráficos** clase que se define en el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **Microsoft.ReportDesigner** espacio de nombres es una implementación paso a través de la <xref:System.Windows.Forms.Design.Behavior.Adorner> encontrar la clase en formularios Windows Forms. Para obtener documentación completa sobre la **adorno** de clases, consulte [Introducción al servicio de comportamiento](http://go.microsoft.com/fwlink/?LinkId=116673) en MSDN library. Para el código de ejemplo que implementa un **Microsoft.ReportDesigner.Design.Adornment** de clases, consulte [muestras de producto de SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
 Para obtener más información acerca de cómo programar y usar Windows Forms en [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], vea estos temas en MSDN Library:  
  
-   Atributos de tiempo de diseño para componentes  
  
-   Componentes de[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]  
  
-   Tutorial: Crear un control de Windows Forms que aproveche las características de tiempo de diseño de Visual Studio  
  
## <a name="see-also"></a>Vea también  
 [Arquitectura de elementos de informe personalizado](../../reporting-services/custom-report-items/custom-report-item-architecture.md)   
 [Crear un componente de tiempo de ejecución del elemento de informe personalizado](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [Bibliotecas de clases de elemento de informe personalizado](../../reporting-services/custom-report-items/custom-report-item-class-libraries.md)   
 [Cómo implementar un elemento de informe personalizado](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)  
  
  

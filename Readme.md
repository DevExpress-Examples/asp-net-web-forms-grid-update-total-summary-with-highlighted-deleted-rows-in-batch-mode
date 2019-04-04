<!-- default file list -->
*Files to look at*:

* [Default.aspx](./CS/Default.aspx) (VB: [Default.aspx](./VB/Default.aspx))
* [Default.aspx.cs](./CS/Default.aspx.cs) (VB: [Default.aspx.vb](./VB/Default.aspx.vb))
<!-- default file list end -->
# ASPxGridView - Batch Editing - How to update summaries when HighlightDeletedRows=true


<p>This example illustrates how to modify the <a href="https://www.devexpress.com/Support/Center/p/T114923">ASPxGridView - How to update total summaries on the client side in Batch Edit mode</a> example to correctly calculate the total summary if the <a href="https://documentation.devexpress.com/#AspNet/DevExpressWebGridViewBatchEditSettings_HighlightDeletedRowstopic">GridViewBatchEditSettings.HighlightDeletedRows</a> property is enabled. <br><br></p>
<p><strong>See Also:</strong></p>
<p><a href="https://www.devexpress.com/Support/Center/p/T114539">ASPxGridView - Batch Edit - How to calculate values on the fly</a> <br><a href="https://www.devexpress.com/Support/Center/p/T116925">ASPxGridView - Batch Edit - How to calculate unbound column and total summary values on the fly</a> <br><br><strong>ASP.NET MVC Example:</strong><br><a href="https://www.devexpress.com/Support/Center/p/T137186">GridView - How to update total summaries on the client side in Batch Edit mode</a></p>


<h3>Description</h3>

<p>For this,&nbsp;create a custom Recovery button:</p>
<code lang="aspx">&lt;dx:GridViewCommandColumn ShowNewButtonInHeader="true" ShowDeleteButton="true"&gt;
    &lt;CustomButtons&gt;
        &lt;dx:GridViewCommandColumnCustomButton ID="customRecover" Text="Recover"&gt;&lt;/dx:GridViewCommandColumnCustomButton&gt;
    &lt;/CustomButtons&gt;
&lt;/dx:GridViewCommandColumn&gt;
</code>
<p>&nbsp;To manipulate the button visibility, add the following custom CSS classes:</p>
<code lang="aspx">&lt;Styles&gt;
    &lt;CommandColumnItem CssClass="commandCell"&gt;&lt;/CommandColumnItem&gt;
    &lt;BatchEditDeletedRow CssClass="deletedRow"&gt;&lt;/BatchEditDeletedRow&gt;
&lt;/Styles&gt;
</code>
<p>&nbsp;These CSS rules allow showing a custom Recovery button when it is required:</p>
<code lang="css">.deletedRow a[data-args*="customRecover"].commandCell {
    display: inline !important;
}
a[data-args*="customRecover"].commandCell {
    display: none;
}
</code>
<p>&nbsp;To hide the standard Recovery button, use the following rule:</p>
<code lang="css">a[data-args*="Recover"].commandCell {
    display: none;
}
</code>
<p>&nbsp;Finally, handle the&nbsp;<a href="https://documentation.devexpress.com/#AspNet/DevExpressWebScriptsASPxClientGridView_CustomButtonClicktopic">ASPxClientGridView.CustomButtonClick</a>&nbsp;event to restore the row and calculate the total summary after that:&nbsp;</p>
<code lang="js">function OnCustomButtonClick(s, e) {
    if (e.buttonID == 'customRecover') {
        s.batchEditApi.ResetChanges(e.visibleIndex);
        var value = s.batchEditApi.GetCellValue(e.visibleIndex, "C2");
        labelSum.SetValue((parseFloat(labelSum.GetValue()) + value).toFixed(1));
    }
}
</code>
<p>&nbsp;</p>

<br/>



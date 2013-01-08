---
layout: post
title: "TIL => ReportViewer Control, Less is More"
date: 2013-01-07 21:32
comments: true
categories: [WebForms, MVC, TIL]
---

## TIL: ReportViewer WebControl => Less is More

Stop me if you've heard this one: "Their IT staff is going to take care of that development ..." And so it was recently on a project I am developing. 

A separate development activity was spun up to create the required SSRS reports which were to be hosted on a Report Server. Well the Report Server uses Active Directory accounts for authentication and authorization. The portal that I'm building essentially uses the ASP.net Membership Provider and its services.

Suddenly, I was confronted with a situation where I needed to provide access to reports hosted on a report server from my MVC application and handle security for the reports too. Enter the ReportViewer control, hosted in an ASP.net WebForm ASPX page and running remote mode SSRS reports. 

I scrambled to learn how to host the ReportViewer Control and have it render reports in my application. I didn't search long enough to find a fully baked, working sample, but was able to get a report to render based on an initial set of parameters. I was happy and smug as a bug in a rug. But then I find out that this report should page and sort and link through to other reports. Now I'm a sad panda.

For my first attempt to host the ReportViewer control, I tried to juggle the parameters and update the report URL on each request. As it turns out, I was doing that wrong and completely broke the drill-through reports, paging and searching. After about half a day of combing the Internet for the secrets to keeping the remote reports fully functioning and not finding much helpful, I started to experiment.



``` C# Here is what I ended up with in the WebForm code-behind:
protected override void OnInit(EventArgs e)
{
    base.OnInit(e);
    ReportViewer1.ProcessingMode = ProcessingMode.Remote;
    ReportViewer1.ServerReport.ReportServerUrl = new Uri("http://Report_Server/Report_Root");
    ReportViewer1.ServerReport.DisplayName = "Report Title";
}
 
protected void Page_Load(object sender, EventArgs e)
{
    if (IsPostBack) return;
    
    var inbound_query_param = Request.RequestContext.RouteData.Values["QueryString_Parameter"].ToString();
    var report_param = new ReportParameter("SSRS_Report_Parameter", inbound_query_param);
    var portalUser = ((UserIdentity)User.Identity);
 
    if (portalUser.Account != account)
    {
        // Log invalid access attempt
    }
 
    ReportViewer1.ServerReport.ReportPath = "/Report_Server_Report_Collection/Recipient Summary Page";
    ReportViewer1.ServerReport.SetParameters(new[] { report_param });
    ReportViewer1.ServerReport.Refresh();
}
```
{% gist 4467831 %}

 wound up doing it setting the report server and report title in the OnInit method of the web-page. I also bound the selection controls to the available options for the current user and wired up the change event handlers. PostBack events that aren't triggered by the selection controls that I added to the web form are ignored by the code behind and the httpHandler for the report viewer control handles the interaction with the SSRS server.

https://gist.github.com/4467831


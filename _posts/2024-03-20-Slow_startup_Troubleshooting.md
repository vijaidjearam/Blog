---
layout: post
date: 2024-03-20 16:38:25
title: Slow startup Troubleshooting
category: windows-finetuning
tags: slow startup windows performance
---
# Slow start up can be troubleshooted via windows performance analysis tool available in windows ADK

## Download the latest version of Windows ADK and install the windows performance toolkit.

![image](https://github.com/vijaidjearam/blog/assets/1507737/4e70471e-5e65-491d-b8f4-2238bd8b2589)

### Windows performance recorder
 - Launch the windows performance recorder
 - Select First level triage and in the resource analysis select CPU usage, Disk IO Activity, File IO activity, Registry IO activity, Networking IO activity and Heap Usage
 - In the Performance Scenario  select Boot from the Dropdown a,d in the detail level select the verbose option from the drop down.
 - ![image](https://github.com/vijaidjearam/blog/assets/1507737/39b496cb-1860-4bc8-950e-56f3382a9385)
 - Click on the start button to capture the trace.
 - Once the trace is completed the file are saved in user/documents/WPRFiles

### Windows performance Analyser
- Launch the windows performance analyser
- Open the WPR file created earlier by the windows performance recorder
- Apply the Boot-Logon-GPO-basic.wpaprofile

<details>
    <summary>Boot-Logon-GPO-basic.wpaprofile</summary>
```xml
       <?xml version="1.0" encoding="utf-8"?>
   <WpaProfileContainer xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="2" xmlns="http://tempuri.org/SerializableElement.xsd">
     <Content xsi:type="WpaProfile2">
       <Sessions>
         <Session Index="0">
           <FileReferences>
             <FileReference FileName="Logon.regions.xml" FileNameBase="Catalog" ServiceMoniker="Regions.{51EF6868-EFEC-42A3-B284-1838673CC095}" />
           </FileReferences>
         </Session>
       </Sessions>
       <Views>
         <SysConfigView Guid="58c0a244-1f64-4127-8a82-d33e5521e99c" IsVisible="true" SessionIndex="0" />
         <View Guid="5b694751-59cf-42c3-883a-68d908ab12fc" IsVisible="true" Title="Analysis">
           <Graphs>
             <Graph Guid="1ce7fd53-2344-4ea8-acd6-1a0722a51427" LayoutStyle="DataTable" Color="#FF005DE0" GraphHeight="125" IsMinimized="false" IsShown="true" IsExpanded="false" HelpText="{}{\rtf1\ansi\ansicpg1252\uc1\htmautsp\deff2{\fonttbl{\f0\fcharset0 Times New Roman;}{\f2\fcharset0 Segoe UI;}}{\colortbl\red0\green0\blue0;\red255\green255\blue255;}\loch\hich\dbch\pard\plain\ltrpar\itap0{\lang1033\fs18\f2\cf0 \cf0\ql{\f2 {\ltrch Lets the application apply user-friendly labels to portions of the trace.}\li0\ri0\sa0\sb0\fi0\ql\par}&#xD;&#xA;}&#xD;&#xA;}">
               <Preset Name="Regions of Interest" BarGraphIntervalCount="50" IsThreadActivityTable="false" GraphColumnCount="16" KeyColumnCount="1" LeftFrozenColumnCount="2" RightFrozenColumnCount="15" InitialFilterQuery="[Region]:~=&quot;User logon&quot;" InitialFilterShouldKeep="true" InitialExpansionQuery="[Region]:~=&quot;User logon&quot;" GraphFilterTopValue="0" GraphFilterThresholdValue="0" HelpText="{}{\rtf1\ansi\ansicpg1252\uc1\htmautsp\deff2{\fonttbl{\f0\fcharset0 Times New Roman;}{\f2\fcharset0 Segoe UI;}}{\colortbl\red0\green0\blue0;\red255\green255\blue255;}\loch\hich\dbch\pard\plain\ltrpar\itap0{\lang1033\fs18\f2\cf0 \cf0\ql{\f2 {\ltrch Uses a Regions of Interest file to apply additional markup to an open trace in WPA. These labels are applied by finding events that define the start and stop of a given region. The XML file contains these regions as well as their events.}\li0\ri0\sa0\sb0\fi0\ql\par}&#xD;&#xA;}&#xD;&#xA;}">
                 <MetadataEntries>
                   <MetadataEntry Guid="052aa8a8-ce86-486b-8cc9-158ac7d27113" Name="Stop Thread" ColumnMetadata="EndThreadId" />
                   <MetadataEntry Guid="93b276b8-d183-41b7-a16e-19eb9373dbf3" Name="Start Time" ColumnMetadata="StartTime" />
                   <MetadataEntry Guid="03facf2d-1d9f-43c7-b8e8-aed46477f348" Name="Stop Time" ColumnMetadata="EndTime" />
                 </MetadataEntries>
                 <HighlightEntries />
                 <Columns>
                   <Column Guid="d96b19f7-d47a-40f3-ba80-fe0b9fae4616" Name="Region" SortPriority="1" Width="300" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="471b850d-c2bc-482d-871d-13fb7c13bd2a" Name="Region Guid" AggregationMode="Count" SortPriority="2" Width="106" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="07ec3178-e4ce-4729-a918-f1cc44ee55b9" Name="Region Friendly Name" SortPriority="3" Width="200" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="cb796d44-2927-5ac1-d231-4b71904c18f5" Name="Thread Name" SortPriority="4" Width="80" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="82ddfdff-ee93-5f35-08ac-4705069618dc" Name="Thread Activity Tag" SortPriority="5" Width="80" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="2818954f-2d30-5569-4510-dade0a5a605c" Name="Annotation" SortPriority="6" Width="80" IsVisible="false">
                     <AnnotationsOptionsParameter>
                       <AnnotationQueryEntries />
                     </AnnotationsOptionsParameter>
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="abfa45ec-ef0f-4fdd-8a6d-1c93a140032b" Name="Duration" AggregationMode="Sum" SortPriority="7" TextAlignment="Right" Width="100" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="d0b2a5cb-1966-4fe9-919f-1383932b2d84" Name="Start Process" SortPriority="8" Width="85" IsVisible="true">
                     <ProcessOptionsParameter />
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="c74dbb74-97bf-4c5a-9b21-d967ce08df00" Name="Start Thread" SortOrder="Ascending" SortPriority="0" TextAlignment="Right" Width="80" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="b9e5e33d-d875-4fb2-b4f9-7e9d14d8d370" Name="Stop Process" SortPriority="9" Width="85" IsVisible="true">
                     <ProcessOptionsParameter />
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="052aa8a8-ce86-486b-8cc9-158ac7d27113" Name="Stop Thread" SortPriority="10" TextAlignment="Right" Width="80" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="0c5cf8cd-9b9e-5798-1a5d-09d429f7fa3c" Name="Field 1" SortPriority="11" Width="80" IsVisible="true" HelpText="Field 1">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="71badd11-26e5-56bc-44ec-12f4cc6a8f3e" Name="Field 2" SortPriority="12" Width="80" IsVisible="true" HelpText="Field 2">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="93b276b8-d183-41b7-a16e-19eb9373dbf3" Name="Start Time" AggregationMode="Min" SortPriority="13" TextAlignment="Right" Width="100" IsVisible="true">
                     <DateTimeTimestampOptionsParameter DateTimeEnabled="false" />
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="03facf2d-1d9f-43c7-b8e8-aed46477f348" Name="Stop Time" AggregationMode="Max" SortPriority="14" TextAlignment="Right" Width="100" IsVisible="true">
                     <DateTimeTimestampOptionsParameter DateTimeEnabled="false" />
                     <ColorQueryEntries />
                   </Column>
                 </Columns>
               </Preset>
             </Graph>
             <Graph Guid="da13748b-71c7-4ba1-a61d-6ae4e527e261" LayoutStyle="All" Color="#FFD3D3D3" GraphHeight="74" IsMinimized="false" IsShown="true" IsExpanded="false">
               <Preset Name="Timeline by Phase" BarGraphIntervalCount="50" IsThreadActivityTable="false" GraphColumnCount="9" KeyColumnCount="2" LeftFrozenColumnCount="1" RightFrozenColumnCount="8" InitialFilterShouldKeep="true" GraphFilterTopValue="0" GraphFilterThresholdValue="0">
                 <MetadataEntries>
                   <MetadataEntry Guid="12020749-a4c5-5ed4-7316-9eefb76c72c9" Name="Start Time" ColumnMetadata="StartTime" />
                   <MetadataEntry Guid="a80e59b2-f58f-543e-18e9-6e8fd4b49a84" Name="End Time" ColumnMetadata="EndTime" />
                 </MetadataEntries>
                 <HighlightEntries />
                 <Columns>
                   <Column Guid="09f9ab65-72c9-5447-c56b-99d749bced3c" Name="Phase Name" SortPriority="1" Width="200" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="cb796d44-2927-5ac1-d231-4b71904c18f5" Name="Thread Name" SortPriority="0" Width="80" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="82ddfdff-ee93-5f35-08ac-4705069618dc" Name="Thread Activity Tag" SortPriority="0" Width="80" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="2818954f-2d30-5569-4510-dade0a5a605c" Name="Annotation" SortPriority="0" Width="80" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="4d7f9f8e-bbe4-5ca7-003d-b982d1642eb9" Name="Phase #" SortPriority="2" TextAlignment="Right" Width="80" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="40fb0280-d775-513b-203f-77a5fb761913" Name="Duration" SortPriority="3" TextAlignment="Right" Width="100" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="ce84d427-a0a7-58d9-0fde-e8d2e84770bc" Name="Table" SortPriority="4" Width="80" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="12020749-a4c5-5ed4-7316-9eefb76c72c9" Name="Start Time" SortOrder="Descending" SortPriority="0" TextAlignment="Right" Width="100" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="a80e59b2-f58f-543e-18e9-6e8fd4b49a84" Name="End Time" SortPriority="6" TextAlignment="Right" Width="100" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                 </Columns>
               </Preset>
             </Graph>
             <Graph Guid="920e6241-3dea-46c4-8e4f-04ce08f62c0a" LayoutStyle="All" Color="#FF005DE0" GraphHeight="26" IsMinimized="false" IsShown="true" IsExpanded="false">
               <Preset Name="Delays By Process, Type" BarGraphIntervalCount="50" IsThreadActivityTable="false" GraphColumnCount="20" KeyColumnCount="2" LeftFrozenColumnCount="7" RightFrozenColumnCount="19" InitialFilterShouldKeep="true" GraphFilterTopValue="0" GraphFilterThresholdValue="0">
                 <MetadataEntries>
                   <MetadataEntry Guid="0dfa0e06-53e6-5312-d642-d98b56f0dc60" Name="Start Time" ColumnMetadata="StartTime" />
                   <MetadataEntry Guid="c7d6a333-a213-5b3c-1cb3-0b7632e9c9ef" Name="End Time" ColumnMetadata="EndTime" />
                   <MetadataEntry Guid="f97e23bf-f7f9-5a95-ef77-3f88e240f318" Name="Thread Id" ColumnMetadata="EndThreadId" />
                 </MetadataEntries>
                 <HighlightEntries />
                 <Columns>
                   <Column Guid="6c8c776e-d434-5624-fcdb-9c753f48995c" Name="Process" SortPriority="1" Width="150" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="df500143-42c5-5c44-c21a-6db72a05aa08" Name="Delay Type" SortPriority="2" Width="122" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="cb796d44-2927-5ac1-d231-4b71904c18f5" Name="Thread Name" SortPriority="0" Width="80" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="82ddfdff-ee93-5f35-08ac-4705069618dc" Name="Thread Activity Tag" SortPriority="0" Width="80" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="2818954f-2d30-5569-4510-dade0a5a605c" Name="Annotation" SortPriority="0" Width="80" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="6b1caff7-daff-59c0-9494-240714cc0d90" Name="Process Id" SortOrder="Ascending" SortPriority="3" TextAlignment="Right" Width="60" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="f97e23bf-f7f9-5a95-ef77-3f88e240f318" Name="Thread Id" SortPriority="4" TextAlignment="Right" Width="60" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="b6c76b2c-d05a-5596-d7ff-b97ce190ae8b" Name="Duration" AggregationMode="Sum" SortOrder="Descending" SortPriority="0" TextAlignment="Right" Width="90" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="03caa086-61b9-5259-f3f6-9ac01c5ccd01" Name="SinceInputRemove (ms)" SortPriority="5" TextAlignment="Right" Width="143" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="f468cec2-4547-5c84-696e-d9f17faa370e" Name="SinceOldestInput (ms)" SortPriority="6" TextAlignment="Right" Width="132" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="06d32d4f-33f2-5982-0ff4-ebc63591a82d" Name="Count" AggregationMode="Count" SortPriority="7" TextAlignment="Right" Width="60" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="654b21d5-b577-5401-7b0e-4c927d33ae9b" Name="Thread Flags" SortOrder="Ascending" SortPriority="10" Width="90" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="18a11f02-48ba-5ee3-0fb4-cec688a659e3" Name="Class Name" SortOrder="Ascending" SortPriority="11" Width="90" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="27ef60ec-b78e-56ea-4483-e7ef26c59d36" Name="Top Level Class Name" SortOrder="Ascending" SortPriority="12" Width="90" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="6059d1b1-29db-5700-3f71-1b95294f142d" Name="Message Id" SortOrder="Ascending" SortPriority="13" TextAlignment="Right" Width="60" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="16ccf420-592c-5a89-fb9c-dca154a4edfd" Name="WParam" SortOrder="Ascending" SortPriority="14" TextAlignment="Right" Width="60" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="a451dc77-20a3-5bd2-bc73-c8ded9b752e2" Name="Program Id" SortOrder="Ascending" SortPriority="15" Width="180" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="0dfa0e06-53e6-5312-d642-d98b56f0dc60" Name="Start Time" AggregationMode="Min" SortPriority="8" TextAlignment="Right" Width="90" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="c7d6a333-a213-5b3c-1cb3-0b7632e9c9ef" Name="End Time" AggregationMode="Max" SortPriority="9" TextAlignment="Right" Width="90" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                 </Columns>
               </Preset>
             </Graph>
             <Graph Guid="ebc77ae6-e73c-4a7c-83fc-fde0fde2de1c" LayoutStyle="All" Color="#FF005DE0" GraphHeight="49" IsMinimized="false" IsShown="true" IsExpanded="false">
               <Preset Name="Tasks by Result" BarGraphIntervalCount="50" IsThreadActivityTable="false" GraphColumnCount="13" KeyColumnCount="3" LeftFrozenColumnCount="4" RightFrozenColumnCount="11" InitialFilterShouldKeep="true" GraphFilterTopValue="0" GraphFilterThresholdValue="0">
                 <MetadataEntries />
                 <HighlightEntries />
                 <Columns>
                   <Column Guid="38abdd1d-825f-40de-83f5-05441fe24f32" Name="Result" SortOrder="Ascending" SortPriority="0" Width="149" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="f1501c22-87ac-4a2c-adec-1b4bfce0daa6" Name="Id" SortPriority="2" Width="120" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="619e6df3-5d38-497e-9fb0-7059e4b82264" Name="Name" SortPriority="3" Width="495" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="cb796d44-2927-5ac1-d231-4b71904c18f5" Name="Thread Name" SortPriority="0" Width="80" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="82ddfdff-ee93-5f35-08ac-4705069618dc" Name="Thread Activity Tag" SortPriority="0" Width="80" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="2818954f-2d30-5569-4510-dade0a5a605c" Name="Annotation" SortPriority="0" Width="80" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="8e30338b-ce1a-487d-859e-15901e9ff5ce" Name="Duration" AggregationMode="Max" SortPriority="7" TextAlignment="Right" Width="120" IsVisible="true">
                     <DurationInViewOptionsParameter TimeStampColumnGuid="6ae12b2e-b49d-48da-ad54-77a258cdc8e3" TimeStampType="Start" InViewEnabled="false" />
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="0b613639-a277-487b-8115-fbde462f7fea" Name="Trigger Type" SortPriority="4" Width="80" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="1ef2a355-3b61-441d-8dc5-31ae46978b04" Name="Failure Code" SortPriority="8" Width="134" CellFormat="x" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="441f5aa9-ac23-461d-836f-cf65154040a7" Name="Trigger Time" SortPriority="5" TextAlignment="Right" Width="120" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="8415fdbd-2cad-48eb-840c-a4ff99001e18" Name="Start Time" AggregationMode="Min" SortOrder="Ascending" SortPriority="1" TextAlignment="Right" Width="120" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="6ae12b2e-b49d-48da-ad54-77a258cdc8e3" Name="End Time" AggregationMode="Max" SortPriority="6" TextAlignment="Right" Width="120" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                 </Columns>
               </Preset>
             </Graph>
           </Graphs>
           <SessionIndices>
             <SessionIndex>0</SessionIndex>
           </SessionIndices>
         </View>
         <View Guid="15c3b2ac-c1bb-4b42-a33a-d8748956c5b5" IsVisible="true" Title="GPO Timeline">
           <Graphs>
             <Graph Guid="04f69f98-176e-4d1c-b44e-97f734996ab8" LayoutStyle="All" Color="#FF005DE0" GraphHeight="125" IsMinimized="false" IsShown="true" IsExpanded="false" HelpText="{}{\rtf1\ansi\ansicpg1252\uc1\htmautsp\deff2{\fonttbl{\f0\fcharset0 Times New Roman;}{\f2\fcharset0 Segoe UI;}}{\colortbl\red0\green0\blue0;\red255\green255\blue255;}\loch\hich\dbch\pard\plain\ltrpar\itap0{\lang1033\fs18\f2\cf0 \cf0\ql{\f2 {\ltrch Shows every event in the trace, including the associated payload fields.}\li0\ri0\sa0\sb0\fi0\ql\par{\f2 \li0\ri0\sa0\sb0\fi0\ql\par{\f2 {\ltrch New capability - graph payload fields!}\li0\ri0\sa0\sb0\fi0\ql\par{\f2 \li0\ri0\sa0\sb0\fi0\ql\par{\f2 {\ltrch 1. Filter down to the event with the payload field you want to graph.}\li0\ri0\sa0\sb0\fi0\ql\par{\f2 {\ltrch 2. Drag the column corresponding to the payload field you want to graph to the right of the blue bar.}\li0\ri0\sa0\sb0\fi0\ql\par{\f2 {\ltrch 3. If the automatic graphing isn't representing your data correctly, go to View Editor and:}\li0\ri0\sa0\sb0\fi0\ql\par{\f2 {\ltrch a. Adjust the aggregation mode for your column, or}\li0\ri0\sa0\sb0\fi0\ql\par{\f2 {\ltrch b. Go to Advanced &gt; Graph Configuration and change your graphing aggregation mode.}\li0\ri0\sa0\sb0\fi0\ql\par}">
               <Preset Name="Activity by Provider, Task, Opcode" BarGraphIntervalCount="50" IsThreadActivityTable="false" GraphColumnCount="37" KeyColumnCount="9" LeftFrozenColumnCount="10" RightFrozenColumnCount="35" InitialFilterShouldKeep="true" GraphFilterTopValue="0" GraphFilterThresholdValue="0" HelpText="{}{\rtf1\ansi\ansicpg1252\uc1\htmautsp\deff2{\fonttbl{\f0\fcharset0 Times New Roman;}{\f2\fcharset0 Segoe UI;}}{\colortbl\red0\green0\blue0;\red255\green255\blue255;}\loch\hich\dbch\pard\plain\ltrpar\itap0{\lang1033\fs18\f2\cf0 \cf0\ql{\f2 {\ltrch Groups all the events by provider, task, and opcode.}\li0\ri0\sa0\sb0\fi0\ql\par}&#xD;&#xA;}&#xD;&#xA;}">
                 <MetadataEntries>
                   <MetadataEntry Guid="edf01e5d-3644-4dbc-ab9d-f8954e6db6ea" Name="ThreadId" ColumnMetadata="EndThreadId" />
                   <MetadataEntry Guid="bbfc990a-b6c9-4dcd-858b-f040ab4a1efe" Name="Time" ColumnMetadata="StartTime" />
                   <MetadataEntry Guid="bbfc990a-b6c9-4dcd-858b-f040ab4a1efe" Name="Time" ColumnMetadata="EndTime" />
                 </MetadataEntries>
                 <HighlightEntries />
                 <Columns>
                   <Column Guid="0c5cf8cd-9b9e-5798-1a5d-09d429f7fa3c" Name="Field 1" SortPriority="3" Width="231" IsVisible="false" HelpText="Field 1">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="8b4c40f8-0d99-437d-86ab-56ec200137dc" Name="Provider Name" SortPriority="23" Width="205" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="bbfc990a-b6c9-4dcd-858b-f040ab4a1efe" Name="Time" SortPriority="4" TextAlignment="Right" Width="101" IsVisible="true" HelpText="Time">
                     <DateTimeTimestampOptionsParameter DateTimeEnabled="false" />
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="2a23f9b1-65d6-46d2-87b2-72f3606b7f75" Name="Provider Id" SortPriority="28" Width="100" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="511777f7-30ef-4e86-bd0b-0facaf23a0d3" Name="Task Name" SortPriority="24" Width="80" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="5b51716b-b88f-443a-a396-c6316296d5f8" Name="Opcode Name" SortPriority="25" Width="80" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="c72e1c5a-f6db-4c84-8c0b-85989e514075" Name="Id" SortPriority="26" Width="80" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="d446a182-5203-4a29-aca1-4ab9bea0d1b5" Name="Version" SortPriority="5" Width="80" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="b51bcda1-7ea3-4409-b4af-51a704893bd9" Name="Process Id" SortPriority="6" Width="50" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="cb796d44-2927-5ac1-d231-4b71904c18f5" Name="Thread Name" SortPriority="7" Width="80" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="82ddfdff-ee93-5f35-08ac-4705069618dc" Name="Thread Activity Tag" SortPriority="8" Width="80" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="2818954f-2d30-5569-4510-dade0a5a605c" Name="Annotation" SortPriority="9" Width="80" IsVisible="false">
                     <AnnotationsOptionsParameter>
                       <AnnotationQueryEntries />
                     </AnnotationsOptionsParameter>
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="72892fbe-0f55-426a-9aa1-26b6baf09ffb" Name="Event Type" SortPriority="29" Width="100" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="0734f1a4-fbd9-4ff6-aec0-cf43875c8253" Name="Message" SortPriority="30" Width="100" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="7ee6a5ff-1faf-428a-a7c2-7d2cb2b5cf26" Name="Process" SortPriority="33" Width="124" IsVisible="true">
                     <ProcessOptionsParameter />
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="3be8610c-babb-4154-9970-1b2210928024" Name="Cpu" SortPriority="31" Width="43" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="edf01e5d-3644-4dbc-ab9d-f8954e6db6ea" Name="ThreadId" SortPriority="32" Width="63" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="90fe0b49-e3bb-440f-b829-5813c42108a1" Name="Event Name" SortPriority="27" Width="260" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="0c5cf8cd-9b9e-5798-1a5d-09d429f7fa3c" Name="Field 1" SortPriority="10" Width="167" IsVisible="true" HelpText="Field 1">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="71badd11-26e5-56bc-44ec-12f4cc6a8f3e" Name="Field 2" SortPriority="11" Width="243" IsVisible="true" HelpText="Field 2">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="411dba2d-5d6e-5272-8287-636d0841768c" Name="Field 3" SortPriority="12" Width="80" IsVisible="true" HelpText="Field 3">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="048f5050-1f17-59b3-fa22-4b0781ee630b" Name="Field 4" SortPriority="13" Width="80" IsVisible="true" HelpText="Field 4">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="94e48f22-d499-5227-bb04-be011b4159b0" Name="Field 5" SortPriority="14" Width="80" IsVisible="true" HelpText="Field 5">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="c1054028-424a-59ba-e760-6d30abbd69c5" Name="Field 6" SortPriority="15" Width="80" IsVisible="true" HelpText="Field 6">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="5cbc4b58-2de1-5449-55b2-4651d4edf90a" Name="Field 7" SortPriority="16" Width="80" IsVisible="true" HelpText="Field 7">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="fc01e6c9-a43b-51a1-fd2e-112ba48aff65" Name="Field 8" SortPriority="17" Width="80" IsVisible="true" HelpText="Field 8">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="e3dcf300-46e2-5c43-ef4b-2c3db489ec25" Name="Field 9" SortPriority="18" Width="80" IsVisible="true" HelpText="Field 9">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="87c21ddb-4b29-58e3-5ddc-f114c5ca209a" Name="Field 10" SortPriority="19" Width="80" IsVisible="true" HelpText="Field 10">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="65f8fe42-ad02-5016-3521-f93329c76227" Name="Field 11" SortPriority="20" Width="80" IsVisible="true" HelpText="Field 11">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="03d48fd3-0fe4-57f5-a477-49beb0d70a1f" Name="Field 12" SortPriority="21" Width="80" IsVisible="true" HelpText="Field 12">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="998f8e2d-0f5a-5a54-0133-226e2de62c0b" Name="Field 13" SortPriority="22" Width="80" IsVisible="true" HelpText="Field 13">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="bb772c34-9600-5bf7-3f54-e6080f8a0611" Name="Field 14" SortPriority="1" Width="80" IsVisible="true" HelpText="Field 14">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="1479add7-3dcb-580b-f1e9-87d5186ced61" Name="Field 15" SortPriority="2" Width="80" IsVisible="true" HelpText="Field 15">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="342f7677-17b2-4c7e-b9ec-e89612c49792" Name="Count" AggregationMode="Sum" SortOrder="Descending" SortPriority="0" Width="80" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="bbfc990a-b6c9-4dcd-858b-f040ab4a1efe" Name="Time" SortPriority="34" Width="80" IsVisible="true" HelpText="Time">
                     <DateTimeTimestampOptionsParameter DateTimeEnabled="false" />
                     <ColorQueryEntries />
                   </Column>
                 </Columns>
               </Preset>
             </Graph>
           </Graphs>
           <SessionIndices>
             <SessionIndex>0</SessionIndex>
           </SessionIndices>
         </View>
         <View Guid="c06904f4-52c5-45fe-a373-d0da8bbf5c28" IsVisible="true" Title="Winlogon Timeline">
           <Graphs>
             <Graph Guid="04f69f98-176e-4d1c-b44e-97f734996ab8" LayoutStyle="All" Color="#FF005DE0" GraphHeight="125" IsMinimized="false" IsShown="true" IsExpanded="false" HelpText="{}{\rtf1\ansi\ansicpg1252\uc1\htmautsp\deff2{\fonttbl{\f0\fcharset0 Times New Roman;}{\f2\fcharset0 Segoe UI;}}{\colortbl\red0\green0\blue0;\red255\green255\blue255;}\loch\hich\dbch\pard\plain\ltrpar\itap0{\lang1033\fs18\f2\cf0 \cf0\ql{\f2 {\ltrch Shows every event in the trace, including the associated payload fields.}\li0\ri0\sa0\sb0\fi0\ql\par{\f2 \li0\ri0\sa0\sb0\fi0\ql\par{\f2 {\ltrch New capability - graph payload fields!}\li0\ri0\sa0\sb0\fi0\ql\par{\f2 \li0\ri0\sa0\sb0\fi0\ql\par{\f2 {\ltrch 1. Filter down to the event with the payload field you want to graph.}\li0\ri0\sa0\sb0\fi0\ql\par{\f2 {\ltrch 2. Drag the column corresponding to the payload field you want to graph to the right of the blue bar.}\li0\ri0\sa0\sb0\fi0\ql\par{\f2 {\ltrch 3. If the automatic graphing isn't representing your data correctly, go to View Editor and:}\li0\ri0\sa0\sb0\fi0\ql\par{\f2 {\ltrch a. Adjust the aggregation mode for your column, or}\li0\ri0\sa0\sb0\fi0\ql\par{\f2 {\ltrch b. Go to Advanced &gt; Graph Configuration and change your graphing aggregation mode.}\li0\ri0\sa0\sb0\fi0\ql\par}">
               <Preset Name="Activity by Provider, Task, Opcode" BarGraphIntervalCount="50" IsThreadActivityTable="false" GraphColumnCount="36" KeyColumnCount="8" LeftFrozenColumnCount="9" RightFrozenColumnCount="34" InitialFilterShouldKeep="true" GraphFilterTopValue="0" GraphFilterThresholdValue="0" HelpText="{}{\rtf1\ansi\ansicpg1252\uc1\htmautsp\deff2{\fonttbl{\f0\fcharset0 Times New Roman;}{\f2\fcharset0 Segoe UI;}}{\colortbl\red0\green0\blue0;\red255\green255\blue255;}\loch\hich\dbch\pard\plain\ltrpar\itap0{\lang1033\fs18\f2\cf0 \cf0\ql{\f2 {\ltrch Groups all the events by provider, task, and opcode.}\li0\ri0\sa0\sb0\fi0\ql\par}&#xD;&#xA;}&#xD;&#xA;}">
                 <MetadataEntries>
                   <MetadataEntry Guid="edf01e5d-3644-4dbc-ab9d-f8954e6db6ea" Name="ThreadId" ColumnMetadata="EndThreadId" />
                   <MetadataEntry Guid="bbfc990a-b6c9-4dcd-858b-f040ab4a1efe" Name="Time" ColumnMetadata="StartTime" />
                   <MetadataEntry Guid="bbfc990a-b6c9-4dcd-858b-f040ab4a1efe" Name="Time" ColumnMetadata="EndTime" />
                 </MetadataEntries>
                 <HighlightEntries />
                 <Columns>
                   <Column Guid="8b4c40f8-0d99-437d-86ab-56ec200137dc" Name="Provider Name" SortPriority="3" Width="306" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="bbfc990a-b6c9-4dcd-858b-f040ab4a1efe" Name="Time" SortOrder="Ascending" SortPriority="0" TextAlignment="Right" Width="114" IsVisible="true" HelpText="Time">
                     <DateTimeTimestampOptionsParameter DateTimeEnabled="false" />
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="2a23f9b1-65d6-46d2-87b2-72f3606b7f75" Name="Provider Id" SortPriority="4" Width="100" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="511777f7-30ef-4e86-bd0b-0facaf23a0d3" Name="Task Name" SortPriority="5" Width="195" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="5b51716b-b88f-443a-a396-c6316296d5f8" Name="Opcode Name" SortPriority="6" Width="80" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="c72e1c5a-f6db-4c84-8c0b-85989e514075" Name="Id" SortPriority="7" Width="80" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="d446a182-5203-4a29-aca1-4ab9bea0d1b5" Name="Version" SortPriority="8" Width="80" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="b51bcda1-7ea3-4409-b4af-51a704893bd9" Name="Process Id" SortPriority="9" Width="50" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="cb796d44-2927-5ac1-d231-4b71904c18f5" Name="Thread Name" SortPriority="10" Width="80" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="82ddfdff-ee93-5f35-08ac-4705069618dc" Name="Thread Activity Tag" SortPriority="11" Width="80" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="2818954f-2d30-5569-4510-dade0a5a605c" Name="Annotation" SortPriority="12" Width="80" IsVisible="false">
                     <AnnotationsOptionsParameter>
                       <AnnotationQueryEntries />
                     </AnnotationsOptionsParameter>
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="7ee6a5ff-1faf-428a-a7c2-7d2cb2b5cf26" Name="Process" SortPriority="13" Width="105" IsVisible="true">
                     <ProcessOptionsParameter />
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="3be8610c-babb-4154-9970-1b2210928024" Name="Cpu" SortPriority="14" Width="35" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="edf01e5d-3644-4dbc-ab9d-f8954e6db6ea" Name="ThreadId" SortPriority="15" Width="59" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="71badd11-26e5-56bc-44ec-12f4cc6a8f3e" Name="Field 2" SortPriority="16" Width="148" IsVisible="true" HelpText="Field 2">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="90fe0b49-e3bb-440f-b829-5813c42108a1" Name="Event Name" SortPriority="17" Width="408" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="72892fbe-0f55-426a-9aa1-26b6baf09ffb" Name="Event Type" SortPriority="18" Width="100" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="0734f1a4-fbd9-4ff6-aec0-cf43875c8253" Name="Message" SortPriority="19" Width="100" IsVisible="false">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="0c5cf8cd-9b9e-5798-1a5d-09d429f7fa3c" Name="Field 1" SortPriority="20" Width="80" IsVisible="true" HelpText="Field 1">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="411dba2d-5d6e-5272-8287-636d0841768c" Name="Field 3" SortPriority="21" Width="80" IsVisible="true" HelpText="Field 3">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="048f5050-1f17-59b3-fa22-4b0781ee630b" Name="Field 4" SortPriority="22" Width="80" IsVisible="true" HelpText="Field 4">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="94e48f22-d499-5227-bb04-be011b4159b0" Name="Field 5" SortPriority="23" Width="80" IsVisible="true" HelpText="Field 5">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="c1054028-424a-59ba-e760-6d30abbd69c5" Name="Field 6" SortPriority="24" Width="80" IsVisible="true" HelpText="Field 6">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="5cbc4b58-2de1-5449-55b2-4651d4edf90a" Name="Field 7" SortPriority="25" Width="80" IsVisible="true" HelpText="Field 7">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="fc01e6c9-a43b-51a1-fd2e-112ba48aff65" Name="Field 8" SortPriority="26" Width="80" IsVisible="true" HelpText="Field 8">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="e3dcf300-46e2-5c43-ef4b-2c3db489ec25" Name="Field 9" SortPriority="27" Width="80" IsVisible="true" HelpText="Field 9">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="87c21ddb-4b29-58e3-5ddc-f114c5ca209a" Name="Field 10" SortPriority="28" Width="80" IsVisible="true" HelpText="Field 10">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="65f8fe42-ad02-5016-3521-f93329c76227" Name="Field 11" SortPriority="29" Width="80" IsVisible="true" HelpText="Field 11">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="03d48fd3-0fe4-57f5-a477-49beb0d70a1f" Name="Field 12" SortPriority="30" Width="80" IsVisible="true" HelpText="Field 12">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="998f8e2d-0f5a-5a54-0133-226e2de62c0b" Name="Field 13" SortPriority="31" Width="80" IsVisible="true" HelpText="Field 13">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="bb772c34-9600-5bf7-3f54-e6080f8a0611" Name="Field 14" SortPriority="1" Width="80" IsVisible="true" HelpText="Field 14">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="1479add7-3dcb-580b-f1e9-87d5186ced61" Name="Field 15" SortPriority="2" Width="80" IsVisible="true" HelpText="Field 15">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="342f7677-17b2-4c7e-b9ec-e89612c49792" Name="Count" AggregationMode="Sum" SortPriority="32" Width="80" IsVisible="true">
                     <ColorQueryEntries />
                   </Column>
                   <Column Guid="bbfc990a-b6c9-4dcd-858b-f040ab4a1efe" Name="Time" SortPriority="33" Width="80" IsVisible="true" HelpText="Time">
                     <DateTimeTimestampOptionsParameter DateTimeEnabled="false" />
                     <ColorQueryEntries />
                   </Column>
                 </Columns>
               </Preset>
             </Graph>
           </Graphs>
           <SessionIndices>
             <SessionIndex>0</SessionIndex>
           </SessionIndices>
         </View>
       </Views>
       <ModifiedGraphs>
         <GraphSchema Guid="04f69f98-176e-4d1c-b44e-97f734996ab8" HelpText="{}{\rtf1\ansi\ansicpg1252\uc1\htmautsp\deff2{\fonttbl{\f0\fcharset0 Times New Roman;}{\f2\fcharset0 Segoe UI;}}{\colortbl\red0\green0\blue0;\red255\green255\blue255;}\loch\hich\dbch\pard\plain\ltrpar\itap0{\lang1033\fs18\f2\cf0 \cf0\ql{\f2 {\ltrch Shows every event in the trace, including the associated payload fields.}\li0\ri0\sa0\sb0\fi0\ql\par{\f2 \li0\ri0\sa0\sb0\fi0\ql\par{\f2 {\ltrch New capability - graph payload fields!}\li0\ri0\sa0\sb0\fi0\ql\par{\f2 \li0\ri0\sa0\sb0\fi0\ql\par{\f2 {\ltrch 1. Filter down to the event with the payload field you want to graph.}\li0\ri0\sa0\sb0\fi0\ql\par{\f2 {\ltrch 2. Drag the column corresponding to the payload field you want to graph to the right of the blue bar.}\li0\ri0\sa0\sb0\fi0\ql\par{\f2 {\ltrch 3. If the automatic graphing isn't representing your data correctly, go to View Editor and:}\li0\ri0\sa0\sb0\fi0\ql\par{\f2 {\ltrch a. Adjust the aggregation mode for your column, or}\li0\ri0\sa0\sb0\fi0\ql\par{\f2 {\ltrch b. Go to Advanced &gt; Graph Configuration and change your graphing aggregation mode.}\li0\ri0\sa0\sb0\fi0\ql\par}">
           <ModifiedPresets />
           <PersistedPresets>
             <Preset Name="Activity by Provider, Task, Opcode" BarGraphIntervalCount="50" IsThreadActivityTable="false" GraphColumnCount="36" KeyColumnCount="8" LeftFrozenColumnCount="9" RightFrozenColumnCount="34" InitialFilterShouldKeep="true" GraphFilterTopValue="0" GraphFilterThresholdValue="0" HelpText="{}{\rtf1\ansi\ansicpg1252\uc1\htmautsp\deff2{\fonttbl{\f0\fcharset0 Times New Roman;}{\f2\fcharset0 Segoe UI;}}{\colortbl\red0\green0\blue0;\red255\green255\blue255;}\loch\hich\dbch\pard\plain\ltrpar\itap0{\lang1033\fs18\f2\cf0 \cf0\ql{\f2 {\ltrch Groups all the events by provider, task, and opcode.}\li0\ri0\sa0\sb0\fi0\ql\par}&#xD;&#xA;}&#xD;&#xA;}">
               <MetadataEntries>
                 <MetadataEntry Guid="edf01e5d-3644-4dbc-ab9d-f8954e6db6ea" Name="ThreadId" ColumnMetadata="EndThreadId" />
                 <MetadataEntry Guid="bbfc990a-b6c9-4dcd-858b-f040ab4a1efe" Name="Time" ColumnMetadata="StartTime" />
                 <MetadataEntry Guid="bbfc990a-b6c9-4dcd-858b-f040ab4a1efe" Name="Time" ColumnMetadata="EndTime" />
               </MetadataEntries>
               <HighlightEntries />
               <Columns>
                 <Column Guid="8b4c40f8-0d99-437d-86ab-56ec200137dc" Name="Provider Name" SortPriority="3" Width="306" IsVisible="false">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="bbfc990a-b6c9-4dcd-858b-f040ab4a1efe" Name="Time" SortOrder="Ascending" SortPriority="0" TextAlignment="Right" Width="114" IsVisible="true" HelpText="Time">
                   <DateTimeTimestampOptionsParameter DateTimeEnabled="false" />
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="2a23f9b1-65d6-46d2-87b2-72f3606b7f75" Name="Provider Id" SortPriority="4" Width="100" IsVisible="false">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="511777f7-30ef-4e86-bd0b-0facaf23a0d3" Name="Task Name" SortPriority="5" Width="195" IsVisible="true">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="5b51716b-b88f-443a-a396-c6316296d5f8" Name="Opcode Name" SortPriority="6" Width="80" IsVisible="false">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="c72e1c5a-f6db-4c84-8c0b-85989e514075" Name="Id" SortPriority="7" Width="80" IsVisible="false">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="d446a182-5203-4a29-aca1-4ab9bea0d1b5" Name="Version" SortPriority="8" Width="80" IsVisible="false">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="b51bcda1-7ea3-4409-b4af-51a704893bd9" Name="Process Id" SortPriority="9" Width="50" IsVisible="false">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="cb796d44-2927-5ac1-d231-4b71904c18f5" Name="Thread Name" SortPriority="10" Width="80" IsVisible="false">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="82ddfdff-ee93-5f35-08ac-4705069618dc" Name="Thread Activity Tag" SortPriority="11" Width="80" IsVisible="false">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="2818954f-2d30-5569-4510-dade0a5a605c" Name="Annotation" SortPriority="12" Width="80" IsVisible="false">
                   <AnnotationsOptionsParameter>
                     <AnnotationQueryEntries />
                   </AnnotationsOptionsParameter>
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="7ee6a5ff-1faf-428a-a7c2-7d2cb2b5cf26" Name="Process" SortPriority="13" Width="105" IsVisible="true">
                   <ProcessOptionsParameter />
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="3be8610c-babb-4154-9970-1b2210928024" Name="Cpu" SortPriority="14" Width="35" IsVisible="true">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="edf01e5d-3644-4dbc-ab9d-f8954e6db6ea" Name="ThreadId" SortPriority="15" Width="59" IsVisible="true">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="71badd11-26e5-56bc-44ec-12f4cc6a8f3e" Name="Field 2" SortPriority="16" Width="148" IsVisible="true" HelpText="Field 2">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="90fe0b49-e3bb-440f-b829-5813c42108a1" Name="Event Name" SortPriority="17" Width="408" IsVisible="true">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="72892fbe-0f55-426a-9aa1-26b6baf09ffb" Name="Event Type" SortPriority="18" Width="100" IsVisible="false">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="0734f1a4-fbd9-4ff6-aec0-cf43875c8253" Name="Message" SortPriority="19" Width="100" IsVisible="false">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="0c5cf8cd-9b9e-5798-1a5d-09d429f7fa3c" Name="Field 1" SortPriority="20" Width="80" IsVisible="true" HelpText="Field 1">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="411dba2d-5d6e-5272-8287-636d0841768c" Name="Field 3" SortPriority="21" Width="80" IsVisible="true" HelpText="Field 3">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="048f5050-1f17-59b3-fa22-4b0781ee630b" Name="Field 4" SortPriority="22" Width="80" IsVisible="true" HelpText="Field 4">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="94e48f22-d499-5227-bb04-be011b4159b0" Name="Field 5" SortPriority="23" Width="80" IsVisible="true" HelpText="Field 5">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="c1054028-424a-59ba-e760-6d30abbd69c5" Name="Field 6" SortPriority="24" Width="80" IsVisible="true" HelpText="Field 6">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="5cbc4b58-2de1-5449-55b2-4651d4edf90a" Name="Field 7" SortPriority="25" Width="80" IsVisible="true" HelpText="Field 7">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="fc01e6c9-a43b-51a1-fd2e-112ba48aff65" Name="Field 8" SortPriority="26" Width="80" IsVisible="true" HelpText="Field 8">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="e3dcf300-46e2-5c43-ef4b-2c3db489ec25" Name="Field 9" SortPriority="27" Width="80" IsVisible="true" HelpText="Field 9">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="87c21ddb-4b29-58e3-5ddc-f114c5ca209a" Name="Field 10" SortPriority="28" Width="80" IsVisible="true" HelpText="Field 10">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="65f8fe42-ad02-5016-3521-f93329c76227" Name="Field 11" SortPriority="29" Width="80" IsVisible="true" HelpText="Field 11">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="03d48fd3-0fe4-57f5-a477-49beb0d70a1f" Name="Field 12" SortPriority="30" Width="80" IsVisible="true" HelpText="Field 12">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="998f8e2d-0f5a-5a54-0133-226e2de62c0b" Name="Field 13" SortPriority="31" Width="80" IsVisible="true" HelpText="Field 13">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="bb772c34-9600-5bf7-3f54-e6080f8a0611" Name="Field 14" SortPriority="1" Width="80" IsVisible="true" HelpText="Field 14">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="1479add7-3dcb-580b-f1e9-87d5186ced61" Name="Field 15" SortPriority="2" Width="80" IsVisible="true" HelpText="Field 15">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="342f7677-17b2-4c7e-b9ec-e89612c49792" Name="Count" AggregationMode="Sum" SortPriority="32" Width="80" IsVisible="true">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="bbfc990a-b6c9-4dcd-858b-f040ab4a1efe" Name="Time" SortPriority="33" Width="80" IsVisible="true" HelpText="Time">
                   <DateTimeTimestampOptionsParameter DateTimeEnabled="false" />
                   <ColorQueryEntries />
                 </Column>
               </Columns>
             </Preset>
           </PersistedPresets>
         </GraphSchema>
         <GraphSchema Guid="1ce7fd53-2344-4ea8-acd6-1a0722a51427" HelpText="{}{\rtf1\ansi\ansicpg1252\uc1\htmautsp\deff2{\fonttbl{\f0\fcharset0 Times New Roman;}{\f2\fcharset0 Segoe UI;}}{\colortbl\red0\green0\blue0;\red255\green255\blue255;}\loch\hich\dbch\pard\plain\ltrpar\itap0{\lang1033\fs18\f2\cf0 \cf0\ql{\f2 {\ltrch Lets the application apply user-friendly labels to portions of the trace.}\li0\ri0\sa0\sb0\fi0\ql\par}&#xD;&#xA;}&#xD;&#xA;}">
           <ModifiedPresets />
           <PersistedPresets>
             <Preset Name="Regions of Interest" BarGraphIntervalCount="50" IsThreadActivityTable="false" GraphColumnCount="16" KeyColumnCount="1" LeftFrozenColumnCount="2" RightFrozenColumnCount="15" InitialFilterQuery="[Region]:~=&quot;User logon&quot;" InitialFilterShouldKeep="true" InitialExpansionQuery="[Region]:~=&quot;User logon&quot;" GraphFilterTopValue="0" GraphFilterThresholdValue="0" HelpText="{}{\rtf1\ansi\ansicpg1252\uc1\htmautsp\deff2{\fonttbl{\f0\fcharset0 Times New Roman;}{\f2\fcharset0 Segoe UI;}}{\colortbl\red0\green0\blue0;\red255\green255\blue255;}\loch\hich\dbch\pard\plain\ltrpar\itap0{\lang1033\fs18\f2\cf0 \cf0\ql{\f2 {\ltrch Uses a Regions of Interest file to apply additional markup to an open trace in WPA. These labels are applied by finding events that define the start and stop of a given region. The XML file contains these regions as well as their events.}\li0\ri0\sa0\sb0\fi0\ql\par}&#xD;&#xA;}&#xD;&#xA;}">
               <MetadataEntries>
                 <MetadataEntry Guid="052aa8a8-ce86-486b-8cc9-158ac7d27113" Name="Stop Thread" ColumnMetadata="EndThreadId" />
                 <MetadataEntry Guid="93b276b8-d183-41b7-a16e-19eb9373dbf3" Name="Start Time" ColumnMetadata="StartTime" />
                 <MetadataEntry Guid="03facf2d-1d9f-43c7-b8e8-aed46477f348" Name="Stop Time" ColumnMetadata="EndTime" />
               </MetadataEntries>
               <HighlightEntries />
               <Columns>
                 <Column Guid="d96b19f7-d47a-40f3-ba80-fe0b9fae4616" Name="Region" SortPriority="1" Width="300" IsVisible="true">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="471b850d-c2bc-482d-871d-13fb7c13bd2a" Name="Region Guid" AggregationMode="Count" SortPriority="2" Width="106" IsVisible="true">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="07ec3178-e4ce-4729-a918-f1cc44ee55b9" Name="Region Friendly Name" SortPriority="3" Width="200" IsVisible="false">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="cb796d44-2927-5ac1-d231-4b71904c18f5" Name="Thread Name" SortPriority="4" Width="80" IsVisible="false">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="82ddfdff-ee93-5f35-08ac-4705069618dc" Name="Thread Activity Tag" SortPriority="5" Width="80" IsVisible="false">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="2818954f-2d30-5569-4510-dade0a5a605c" Name="Annotation" SortPriority="6" Width="80" IsVisible="false">
                   <AnnotationsOptionsParameter>
                     <AnnotationQueryEntries />
                   </AnnotationsOptionsParameter>
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="abfa45ec-ef0f-4fdd-8a6d-1c93a140032b" Name="Duration" AggregationMode="Sum" SortPriority="7" TextAlignment="Right" Width="100" IsVisible="true">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="d0b2a5cb-1966-4fe9-919f-1383932b2d84" Name="Start Process" SortPriority="8" Width="85" IsVisible="true">
                   <ProcessOptionsParameter />
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="c74dbb74-97bf-4c5a-9b21-d967ce08df00" Name="Start Thread" SortOrder="Ascending" SortPriority="0" TextAlignment="Right" Width="80" IsVisible="true">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="b9e5e33d-d875-4fb2-b4f9-7e9d14d8d370" Name="Stop Process" SortPriority="9" Width="85" IsVisible="true">
                   <ProcessOptionsParameter />
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="052aa8a8-ce86-486b-8cc9-158ac7d27113" Name="Stop Thread" SortPriority="10" TextAlignment="Right" Width="80" IsVisible="true">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="0c5cf8cd-9b9e-5798-1a5d-09d429f7fa3c" Name="Field 1" SortPriority="11" Width="80" IsVisible="true" HelpText="Field 1">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="71badd11-26e5-56bc-44ec-12f4cc6a8f3e" Name="Field 2" SortPriority="12" Width="80" IsVisible="true" HelpText="Field 2">
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="93b276b8-d183-41b7-a16e-19eb9373dbf3" Name="Start Time" AggregationMode="Min" SortPriority="13" TextAlignment="Right" Width="100" IsVisible="true">
                   <DateTimeTimestampOptionsParameter DateTimeEnabled="false" />
                   <ColorQueryEntries />
                 </Column>
                 <Column Guid="03facf2d-1d9f-43c7-b8e8-aed46477f348" Name="Stop Time" AggregationMode="Max" SortPriority="14" TextAlignment="Right" Width="100" IsVisible="true">
                   <DateTimeTimestampOptionsParameter DateTimeEnabled="false" />
                   <ColorQueryEntries />
                 </Column>
               </Columns>
             </Preset>
           </PersistedPresets>
         </GraphSchema>
       </ModifiedGraphs>
     </Content>
   </WpaProfileContainer>
   
```
 </details>


  





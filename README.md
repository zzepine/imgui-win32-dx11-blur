# ImGui DX11 Blur
<img width="614" height="360" alt="image" src="https://github.com/user-attachments/assets/c488e76d-83d3-4ef3-b35a-cb8fe938faf1" />


This repository contains Dear ImGui source with blur api for DX11/Win32.

The blur implementation adds a simple API for:
- Window background blur
- Rectangular blur with draw lists

Current blur type is gaussian blur.

## What was added?
- Window flag: ImGuiWindowFlags_BlurredBg
- Style var: ImGuiStyleVar_WindowBgBlur
- Draw list call: ImDrawList::AddBlur(p_min, p_max, amount)

Example usage is in examples/example_win32_directx11/main.cpp

## Usage

### 1) Window background blur
```
ImGui::PushStyleVar(ImGuiStyleVar_WindowBgBlur, 0.1f);
if (ImGui::Begin("Blurred Background Window", nullptr, ImGuiWindowFlags_BlurredBg))
{
    ImGui::Text("This window has a blurred background!");
}
ImGui::End();
ImGui::PopStyleVar();
```
or if you want to set it globally for all windows:
```
ImGuiStyle& style = ImGui::GetStyle();
style.WindowBgBlur = 0.1f;
...
if (ImGui::Begin("Blurred Background Window", nullptr, ImGuiWindowFlags_BlurredBg))
{
    ImGui::Text("This window has a blurred background!");
}
ImGui::End();
```

### 2) Rectangular blur
```
ImGui::GetBackgroundDrawList()->AddBlur({ 400.0f, 200.0f }, { 500.0f, 300.0f }, 0.01f);
ImGui::GetForegroundDrawList()->AddBlur({ 400.0f, 400.0f }, { 500.0f, 500.0f }, 0.01f);
```

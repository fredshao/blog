## Unity3D鼠标拖动3D物体移动

> 主要逻辑是使用目标摄像机计算出两个已经距离的世界坐标对应的屏幕坐标，进而计算出每移动1像素，对应在世界中移动多少距离。例如例如目标摄像机计算出(0,0,0)，(1,0,0)两个位置的屏幕坐标sPos1, sPos2，计算出sPos1和sPos2的距离s，也就计算出了世界中移动1米，对应屏坐标移动多少像素，1 / s 得出每移动1像素，对应世界中移动多少米。

代码如下：
```c#
using System;
using System.Collections.Generic;
using UnityEngine;


public class GameObjectDrag : MonoBehaviour
{
    private Vector3 startMousePos;
    private Vector3 startTransPos;
    private float meterPerPixel = 0.0f;

    private void Awake()
    {
        // 这里是查找摄像机，这里可以使用各种方式去赋值摄相机
        GameObject cameraObj = GameObject.Find("TestCamera");
        if(cameraObj == null)
        {
            Debug.LogError("Can not found TestCamera");
            this.enabled = false;
            return;
        }

        Camera cam = cameraObj.GetComponent<Camera>();
        if(cam == null)
        {
            Debug.LogError("Get Camera Component is NULL");
            this.enabled = false;
            return;
        }

        CalculateMoveUnit(cam);
    }

    // 计算出屏幕上每移动1像素，对应世界中移动多少距离
    private void CalculateMoveUnit(Camera _camera)
    {
        Vector3 pos1 = new Vector3(0, 0, 0);
        Vector3 pos2 = new Vector3(1, 0, 0);

        Vector3 sPos1 = _camera.WorldToScreenPoint(pos1);
        Vector3 sPos2 = _camera.WorldToScreenPoint(pos2);
        float pixelPerMeter = (sPos2 - sPos1).magnitude;
        float meterPerPixel = 1.0f / pixelPerMeter;
        this.meterPerPixel = meterPerPixel;
    }

    private void OnMouseDown()
    {
        startMousePos = Input.mousePosition;
        startTransPos = transform.position;
    }

    public void OnMouseUp()
    {
        HandleDrag();
    }

    public void OnMouseDrag()
    {
        HandleDrag();
    }

    private void HandleDrag()
    {
        transform.position = CalculateCurrentPos();
    }

    // 计算出最新的世界坐标
    private Vector3 CalculateCurrentPos()
    {
        Vector3 currMousePos = Input.mousePosition;
        Vector3 dir = (currMousePos - startMousePos).normalized;
        float movedPixel = (currMousePos - startMousePos).magnitude;
        float movedMeter = movedPixel * meterPerPixel;
        Vector3 currPos = startTransPos + dir * movedMeter;
        return currPos;
    }
}
```
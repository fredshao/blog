##### UGUI RectTransform跟随3D GameObject(世界转屏幕坐标)

```c#
// 返回的屏幕坐标用于Anchor在屏幕中心的RectTransform
public Vector2 PlaceParticlesOnPosition(Transform _target, RectTransform canvasRect)
    {

        Vector2 ViewportPosition = Camera.main.WorldToViewportPoint(_target.position);
        Vector2 WorldObject_ScreenPosition = new Vector2(
            ((ViewportPosition.x * canvasRect.sizeDelta.x) - (canvasRect.sizeDelta.x * 0.5f)),
            ((ViewportPosition.y * canvasRect.sizeDelta.y) - (canvasRect.sizeDelta.y * 0.5f)));

        return WorldObject_ScreenPosition;
    }

```


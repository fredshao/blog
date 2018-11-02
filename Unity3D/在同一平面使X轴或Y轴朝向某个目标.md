## 在同一平面使X轴或Y轴朝向某个目标

```c#
private void MakeXForwardTarget()
{
    targetPos = target.position;

    Vector3 currPos = transform.position;
    Vector3 dir = currPos - targetPos;
    float dotValue = Vector3.Dot(-transform.right, dir.normalized);
    float angle = Mathf.Acos(dotValue) * Mathf.Rad2Deg;
    Vector3 tempDir = Vector3.Cross(-transform.right, dir.normalized);
    if (tempDir.z < 0)
    {
        angle *= -1;
    }

    transform.RotateAround(currPos, Vector3.forward, angle);
}


private void MakeYForwardTarget()
{
    targetPos = target.position;

    Vector3 currPos = transform.position;
    Vector3 dir = currPos - targetPos;
    float dotValue = Vector3.Dot(-transform.up, dir.normalized);
    float angle = Mathf.Acos(dotValue) * Mathf.Rad2Deg;
    Vector3 tempDir = Vector3.Cross(-transform.up, dir.normalized);
    if (tempDir.z < 0)
    {
        angle *= -1;
    }
    transform.RotateAround(currPos, Vector3.forward, angle);
}
```


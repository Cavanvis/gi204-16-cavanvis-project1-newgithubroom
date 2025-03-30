using UnityEngine;
using UnityEngine.UI;
using System;

public class PlayerSize : MonoBehaviour
{
    [Header(" Elements ")]
    [SerializeField] private Image fillImage;

    [Header(" Settings ")]
    [SerializeField] private float scaleIncreaseThreshold;
    [SerializeField] private float scaleStep;
    [SerializeField] private AnimationCurve sizeCurve;
    private float scaleValue;

    [Header(" Events ")]
    public static Action<float> onIncrease;

    void Start()
    {
        fillImage.fillAmount = 0;
    }

    void Update()
    {
        
    }

    private void IncreaseScale()
    {
        float targetScale = transform.localScale.x + scaleStep;
        LeanTween.scale(transform.gameObject, targetScale * Vector3.one, .5f * Time.deltaTime * 60).
        setEase(sizeCurve);

        onIncrease?.Invoke(targetScale);

        //transform.localScale += scaleStep * Vector3.one;
    }

    public void CollectibleCollected(float objectSize)
    {
        scaleValue += objectSize;

        if(scaleValue >= scaleIncreaseThreshold)
        {
            IncreaseScale();
            scaleValue = scaleValue % scaleIncreaseThreshold;
        }

        UpdateFillDisplay();
    }

    private void UpdateFillDisplay()
    {
        float targetFillAmount = scaleValue / scaleIncreaseThreshold;

        LeanTween.value(fillImage.fillAmount, targetFillAmount, .2f * Time.deltaTime * 60).
        setOnUpdate((value) => fillImage.fillAmount = value);
    }

}

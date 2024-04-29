
https://github.com/DreamJarsAI/Apply-AI-like-a-Pro/blob/main/7%20Text%20Augmentation%20Using%20nlpaug.ipynb

https://www.youtube.com/watch?v=lpWewl7y57o

https://www.youtube.com/watch?v=HoqlUu_8fWE

https://github.com/Zecoabdo16/Fine-Tuning-trials-for-LLMs-Models


training_args = TrainingArguments(
    output_dir='./',
    overwrite_output_dir=True,
    load_best_model_at_end=True,
    save_total_limit=1,
    evaluation_strategy="steps",
    save_strategy="steps",
    eval_steps= 300,
    save_steps = 300,
    warmup_ratio=0.6,
    learning_rate=5e-6,
    per_device_train_batch_size=1,
    per_device_eval_batch_size=1,
    gradient_accumulation_steps=16,
    num_train_epochs=3,
    report_to='none',
    optim="adafactor",
    metric_for_best_model = 'RMZ',
    seed=42
)

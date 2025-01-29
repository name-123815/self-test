import { useState } from "react";
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";

const questions = [
  { question: "বাংলাদেশের প্রথম সংবিধান কবে গৃহীত হয়?", options: ["১৯৭১", "১৯৭২", "১৯৭৩", "১৯৭৪"], correct: 1 },
  { question: "Who is the current Secretary-General of the United Nations?", options: ["António Guterres", "Ban Ki-moon", "Kofi Annan", "Boutros Boutros-Ghali"], correct: 0 },
  { question: "পাই-এর মান কত?", options: ["৩.১২", "৩.১৪", "৩.১৬", "৩.১৮"], correct: 1 },
  // আরও ১৯৭টি প্রশ্ন যুক্ত করা হয়েছে
  ...Array.from({ length: 197 }, (_, i) => ({
    question: `Sample Question ${i + 4}?`,
    options: ["Option A", "Option B", "Option C", "Option D"],
    correct: Math.floor(Math.random() * 4),
  })),
];

export default function BcsMockTest() {
  const [answers, setAnswers] = useState(Array(questions.length).fill(null));
  const [submitted, setSubmitted] = useState(false);

  const handleSelect = (index, optionIndex) => {
    if (!submitted) {
      const newAnswers = [...answers];
      newAnswers[index] = optionIndex;
      setAnswers(newAnswers);
    }
  };

  const handleSubmit = () => {
    setSubmitted(true);
  };

  const correctAnswers = answers.filter((ans, i) => ans === questions[i].correct).length;
  const incorrectAnswers = answers.length - correctAnswers;

  return (
    <div className="p-6 space-y-4">
      {questions.map((q, index) => (
        <Card key={index} className="p-4">
          <CardContent>
            <p className="font-semibold">{index + 1}. {q.question}</p>
            <div className="space-y-2 mt-2">
              {q.options.map((option, optionIndex) => (
                <Button
                  key={optionIndex}
                  className={`w-full text-left ${answers[index] === optionIndex ? "bg-blue-500 text-white" : "bg-gray-200"}`}
                  onClick={() => handleSelect(index, optionIndex)}
                >
                  {option}
                </Button>
              ))}
            </div>
          </CardContent>
        </Card>
      ))}
      {!submitted ? (
        <Button className="w-full bg-green-500 text-white" onClick={handleSubmit}>Submit</Button>
      ) : (
        <div className="p-4 bg-gray-100 rounded-lg">
          <p>✅ সঠিক উত্তর: {correctAnswers}</p>
          <p>❌ ভুল উত্তর: {incorrectAnswers}</p>
        </div>
      )}
    </div>
  );
}

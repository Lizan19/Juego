import React, { useState } from "react";
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";

const words = [
  "LÍDER", "SOÑADOR", "REALISTA", "CREATIVO", "EMPÁTICO", "CURIOSO",
  "VALIENTE", "PACIENTE", "ENTUSIASTA", "ANALÍTICO"
];

const meanings = {
  LÍDER: "Te gusta tomar la iniciativa y guiar a los demás.",
  SOÑADOR: "Tu mente está llena de ideas e imaginación.",
  REALISTA: "Prefieres lo concreto y lo práctico.",
  CREATIVO: "Ves soluciones donde otros ven problemas.",
  EMPÁTICO: "Puedes ponerte en los zapatos de los demás.",
  CURIOSO: "Siempre estás explorando, preguntando y aprendiendo.",
  VALIENTE: "Enfrentas los desafíos sin miedo.",
  PACIENTE: "Sabes esperar y mantener la calma.",
  ENTUSIASTA: "Tu energía positiva contagia a los demás.",
  ANALÍTICO: "Observas todo con lógica y detalle."
};

function shuffle(array) {
  return array.sort(() => Math.random() - 0.5);
}

export default function DescubreTuPalabraApp() {
  const [shuffledWords, setShuffledWords] = useState(shuffle([...words]));
  const [selected, setSelected] = useState(null);

  const handleSelect = (word) => {
    if (!selected) setSelected(word);
  };

  const handleReset = () => {
    setShuffledWords(shuffle([...words]));
    setSelected(null);
  };

  return (
    <main className="flex flex-col items-center justify-center min-h-screen p-4 bg-gradient-to-br from-purple-100 to-blue-50">
      <h1 className="text-4xl font-extrabold mb-4 text-center">Descubre tu palabra</h1>
      <p className="text-lg text-gray-700 mb-6 max-w-md text-center">
        Mira todas las palabras por unos segundos. ¡Haz clic en la primera que hayas visto para saber qué dice sobre ti!
      </p>

      <div className="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-4 mb-8 w-full max-w-3xl">
        {shuffledWords.map((word, index) => (
          <Card
            key={index}
            onClick={() => handleSelect(word)}
            className={`cursor-pointer transition hover:shadow-xl p-4 text-center text-lg font-semibold rounded-2xl ${selected && selected !== word ? "opacity-30" : "bg-white"}`}
          >
            <CardContent>{word}</CardContent>
          </Card>
        ))}
      </div>

      {selected && (
        <div className="bg-white p-6 rounded-2xl shadow-lg max-w-md text-center">
          <h2 className="text-2xl font-bold mb-2">Tu palabra es: {selected}</h2>
          <p className="text-gray-700 mb-4">{meanings[selected]}</p>
          <Button className="bg-blue-600 hover:bg-blue-700" onClick={handleReset}>Probar otra vez</Button>
        </div>
      )}
    </main>
  );
}

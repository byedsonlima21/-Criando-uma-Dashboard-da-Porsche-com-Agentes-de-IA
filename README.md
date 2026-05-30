# -Criando-uma-Dashboard-da-Porsche-com-Agentes-de-IA
# Porsche Luxury Sales Dashboard

Dashboard executivo desenvolvido como desafio final do curso **Aceleração: AI Reports com Excel, GPT Agents e Claude Code**, da DIO.

O projeto tem como objetivo apresentar uma análise estratégica de vendas da Porsche utilizando uma interface premium inspirada no design oficial da Porsche Brasil, focando em experiência visual refinada, interatividade e insights de negócio.

## Funcionalidades

* Filtros dinâmicos e interativos

  * Modelo da Porsche
  * Ano do modelo
  * Cidade
  * Método de pagamento

* KPIs estratégicos

  * Modelo mais vendido
  * Volume total de vendas
  * Performance por período

* Insights comerciais

  * Carros mais vendidos por cidade
  * Tendências regionais de vendas
  * Identificação de modelos populares

## Tecnologias utilizadas

* React
* Vite
* JavaScript
* Tailwind CSS

## Objetivo do projeto

Este dashboard foi desenvolvido com foco em:

* visualização de dados
* experiência do usuário (UI/UX)
* dashboards executivos
* análise de vendas
* aplicações modernas com IA e automação

## Diferenciais

* Interface inspirada na identidade visual da Porsche Brasil
* Design elegante e minimalista
* Estrutura preparada para expansão com gráficos e integração de dados reais
* Projeto voltado para portfólio de tecnologia e análise de dados

## Autor

Desenvolvido por Edson Lima.


# Codigo

import { useMemo, useState } from 'react';

export default function PorscheDashboard() {
  const rawData = [
    { city: 'São Paulo', model: '911', year: 2024, pay: 'Financing', sales: 12 },
    { city: 'São Paulo', model: 'Cayenne', year: 2023, pay: 'Cash', sales: 9 },
    { city: 'Rio de Janeiro', model: 'Macan', year: 2024, pay: 'Credit', sales: 14 },
    { city: 'Curitiba', model: 'Taycan', year: 2024, pay: 'Financing', sales: 7 },
    { city: 'Belo Horizonte', model: 'Panamera', year: 2023, pay: 'Cash', sales: 5 },
    { city: 'Salvador', model: 'Macan', year: 2024, pay: 'Credit', sales: 10 },
    { city: 'Brasília', model: '911', year: 2025, pay: 'Financing', sales: 11 },
    { city: 'Recife', model: 'Cayenne', year: 2025, pay: 'Cash', sales: 6 },
    { city: 'Fortaleza', model: 'Macan', year: 2025, pay: 'Credit', sales: 13 },
    { city: 'São Paulo', model: 'Taycan', year: 2025, pay: 'Financing', sales: 8 },
  ];

  const [selectedModel, setSelectedModel] = useState('Todos');
  const [selectedYear, setSelectedYear] = useState('Todos');
  const [selectedCity, setSelectedCity] = useState('Todos');
  const [selectedPay, setSelectedPay] = useState('Todos');

  const models = [...new Set(rawData.map((item) => item.model))];
  const years = [...new Set(rawData.map((item) => item.year))];
  const cities = [...new Set(rawData.map((item) => item.city))];
  const payments = [...new Set(rawData.map((item) => item.pay))];

  const filteredData = useMemo(() => {
    return rawData.filter((item) => {
      return (
        (selectedModel === 'Todos' || item.model === selectedModel) &&
        (selectedYear === 'Todos' || item.year === Number(selectedYear)) &&
        (selectedCity === 'Todos' || item.city === selectedCity) &&
        (selectedPay === 'Todos' || item.pay === selectedPay)
      );
    });
  }, [selectedModel, selectedYear, selectedCity, selectedPay]);

  const totalSales = filteredData.reduce((acc, item) => acc + item.sales, 0);

  const topModel = filteredData.length
    ? [...filteredData].sort((a, b) => b.sales - a.sales)[0]
    : null;

  const modelRanking = [...filteredData]
    .sort((a, b) => b.sales - a.sales)
    .slice(0, 5);

  const cityInsights = [
    {
      city: 'São Paulo',
      insight:
        'Modelos esportivos premium apresentam maior saída, especialmente Porsche 911 e Taycan.',
    },
    {
      city: 'Rio de Janeiro',
      insight:
        'Macan domina o volume de vendas devido ao equilíbrio entre luxo e usabilidade urbana.',
    },
    {
      city: 'Fortaleza',
      insight:
        'Crescimento acelerado na procura por SUVs Porsche de entrada e financiamento premium.',
    },
  ];

  return (
    <div className="min-h-screen bg-black text-white p-8 font-sans">
      <div className="max-w-7xl mx-auto">
        <div className="flex flex-col lg:flex-row justify-between items-start lg:items-center gap-6 mb-10 border-b border-zinc-800 pb-6">
          <div>
            <p className="uppercase tracking-[0.4em] text-zinc-400 text-xs mb-3">
              Porsche Brasil Analytics
            </p>
            <h1 className="text-5xl font-light tracking-wide">
              Luxury Sales Dashboard
            </h1>
            <p className="text-zinc-400 mt-4 max-w-2xl leading-relaxed">
              Dashboard executivo inspirado na identidade visual da Porsche Brasil,
              com foco em elegância, minimalismo e inteligência comercial.
            </p>
          </div>

          <div className="bg-zinc-900 border border-zinc-800 rounded-3xl px-6 py-5 shadow-2xl">
            <p className="text-zinc-400 text-sm">Volume total de vendas</p>
            <h2 className="text-4xl font-semibold mt-2">{totalSales}</h2>
          </div>
        </div>

        <div className="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-4 gap-5 mb-10">
          <div className="bg-zinc-950 border border-zinc-800 rounded-3xl p-5">
            <p className="text-zinc-400 text-sm mb-2">Modelo Porsche</p>
            <select
              value={selectedModel}
              onChange={(e) => setSelectedModel(e.target.value)}
              className="w-full bg-black border border-zinc-700 rounded-2xl px-4 py-3 outline-none"
            >
              <option>Todos</option>
              {models.map((model) => (
                <option key={model}>{model}</option>
              ))}
            </select>
          </div>

          <div className="bg-zinc-950 border border-zinc-800 rounded-3xl p-5">
            <p className="text-zinc-400 text-sm mb-2">Model Year</p>
            <select
              value={selectedYear}
              onChange={(e) => setSelectedYear(e.target.value)}
              className="w-full bg-black border border-zinc-700 rounded-2xl px-4 py-3 outline-none"
            >
              <option>Todos</option>
              {years.map((year) => (
                <option key={year}>{year}</option>
              ))}
            </select>
          </div>

          <div className="bg-zinc-950 border border-zinc-800 rounded-3xl p-5">
            <p className="text-zinc-400 text-sm mb-2">Cidade</p>
            <select
              value={selectedCity}
              onChange={(e) => setSelectedCity(e.target.value)}
              className="w-full bg-black border border-zinc-700 rounded-2xl px-4 py-3 outline-none"
            >
              <option>Todos</option>
              {cities.map((city) => (
                <option key={city}>{city}</option>
              ))}
            </select>
          </div>

          <div className="bg-zinc-950 border border-zinc-800 rounded-3xl p-5">
            <p className="text-zinc-400 text-sm mb-2">Pay Method</p>
            <select
              value={selectedPay}
              onChange={(e) => setSelectedPay(e.target.value)}
              className="w-full bg-black border border-zinc-700 rounded-2xl px-4 py-3 outline-none"
            >
              <option>Todos</option>
              {payments.map((payment) => (
                <option key={payment}>{payment}</option>
              ))}
            </select>
          </div>
        </div>

        <div className="grid grid-cols-1 xl:grid-cols-3 gap-6 mb-10">
          <div className="bg-gradient-to-br from-zinc-950 to-zinc-900 border border-zinc-800 rounded-[32px] p-7 shadow-2xl">
            <p className="text-zinc-400 text-sm uppercase tracking-[0.2em]">
              KPI Estratégico
            </p>
            <h3 className="text-3xl font-light mt-4 leading-snug">
              Modelo mais vendido no período
            </h3>
            <div className="mt-8">
              <p className="text-6xl font-semibold">{topModel ? topModel.model : '--'}</p>
              <p className="text-zinc-400 mt-3 text-lg">
                {topModel ? `${topModel.sales} vendas registradas` : 'Nenhum dado encontrado'}
              </p>
            </div>
          </div>

          <div className="xl:col-span-2 bg-zinc-950 border border-zinc-800 rounded-[32px] p-7">
            <div className="flex justify-between items-center mb-6">
              <div>
                <p className="text-zinc-400 text-sm uppercase tracking-[0.2em]">
                  Business Question
                </p>
                <h3 className="text-2xl font-light mt-2">
                  Quais os modelos mais vendidos por cidade?
                </h3>
              </div>
            </div>

            <div className="space-y-4">
              {modelRanking.map((item, index) => (
                <div
                  key={index}
                  className="bg-black border border-zinc-800 rounded-2xl p-5 flex justify-between items-center"
                >
                  <div>
                    <p className="text-xl font-medium">{item.model}</p>
                    <p className="text-zinc-500 mt-1">{item.city}</p>
                  </div>

                  <div className="text-right">
                    <p className="text-3xl font-semibold">{item.sales}</p>
                    <p className="text-zinc-500 text-sm">vendas</p>
                  </div>
                </div>
              ))}
            </div>
          </div>
        </div>

        <div className="grid grid-cols-1 xl:grid-cols-2 gap-6">
          <div className="bg-zinc-950 border border-zinc-800 rounded-[32px] p-7">
            <p className="text-zinc-400 text-sm uppercase tracking-[0.2em]">
              Performance Temporal
            </p>
            <h3 className="text-2xl font-light mt-2 mb-8">
              Qual modelo teve maior saída em um período?
            </h3>

            <div className="space-y-5">
              {rawData.slice(0, 6).map((item, index) => (
                <div key={index}>
                  <div className="flex justify-between mb-2 text-sm">
                    <span>
                      {item.model} • {item.year}
                    </span>
                    <span>{item.sales} vendas</span>
                  </div>

                  <div className="w-full bg-zinc-800 rounded-full h-3 overflow-hidden">
                    <div
                      className="bg-white h-3 rounded-full"
                      style={{ width: `${item.sales * 6}%` }}
                    />
                  </div>
                </div>
              ))}
            </div>
          </div>

          <div className="bg-gradient-to-br from-zinc-950 to-black border border-zinc-800 rounded-[32px] p-7">
            <p className="text-zinc-400 text-sm uppercase tracking-[0.2em]">
              Insights Inteligentes
            </p>
            <h3 className="text-2xl font-light mt-2 mb-8">
              Carros populares por cidade
            </h3>

            <div className="space-y-5">
              {cityInsights.map((item, index) => (
                <div
                  key={index}
                  className="border border-zinc-800 rounded-2xl p-5 bg-zinc-900/40 backdrop-blur"
                >
                  <div className="flex items-center justify-between mb-3">
                    <h4 className="text-xl font-medium">{item.city}</h4>
                    <span className="text-xs uppercase tracking-[0.2em] text-zinc-500">
                      Insight
                    </span>
                  </div>

                  <p className="text-zinc-300 leading-relaxed">
                    {item.insight}
                  </p>
                </div>
              ))}
            </div>
          </div>
        </div>
      </div>
    </div>
  );
}

